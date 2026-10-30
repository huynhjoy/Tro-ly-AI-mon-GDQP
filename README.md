<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>JOY EDU - Tạo Đề Bằng AI</title>
    <!-- Nhúng thư viện Supabase -->
    <script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2"></script>
    <style>
        body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; max-width: 800px; margin: 0 auto; padding: 20px; background-color: #f4f7f6; }
        .container { background: white; padding: 25px; border-radius: 10px; box-shadow: 0 4px 6px rgba(0,0,0,0.1); }
        h1 { color: #2c3e50; text-align: center; }
        textarea { width: 100%; height: 150px; padding: 12px; border: 1px solid #ccc; border-radius: 6px; margin-bottom: 15px; font-size: 15px; box-sizing: border-box; }
        button { background-color: #3498db; color: white; border: none; padding: 12px 20px; font-size: 16px; border-radius: 6px; cursor: pointer; width: 100%; font-weight: bold; transition: background 0.3s; }
        button:hover { background-color: #2980b9; }
        button:disabled { background-color: #95a5a6; cursor: not-allowed; }
        #status { margin-top: 15px; text-align: center; font-style: italic; color: #e67e22; }
        .question-card { background: #f9f9f9; padding: 15px; margin-top: 15px; border-left: 4px solid #27ae60; border-radius: 4px; }
        .options { list-style-type: none; padding-left: 0; }
        .options li { margin: 5px 0; padding: 5px; background: #fff; border: 1px solid #eee; border-radius: 4px; }
        .correct { color: #c0392b; font-weight: bold; margin-top: 10px; }
    </style>
</head>
<body>

<div class="container">
    <h1>JOY EDU - Trợ Lý Tạo Đề GDQP&AN</h1>
    
    <label for="docContent"><b>Nhập nội dung bài học (VD: Kỹ thuật sử dụng lựu đạn):</b></label>
    <textarea id="docContent" placeholder="Dán nội dung văn bản từ SGK hoặc tài liệu vào đây..."></textarea>
    
    <button id="btnGenerate" onclick="processDocument()">Tạo Câu Hỏi Bằng AI & Lưu CSDL</button>
    <div id="status"></div>
    
    <div id="resultArea"></div>
</div>

<script>
    // 1. CẤU HÌNH SUPABASE (Thầy lấy trong mục Project Settings > API của Supabase)
    const SUPABASE_URL = 'https://THAY_BANG_URL_CUA_THAY.supabase.co';
    const SUPABASE_ANON_KEY = 'THAY_BANG_ANON_KEY_CUA_THAY';
    
    const supabase = window.supabase.createClient(SUPABASE_URL, SUPABASE_ANON_KEY);

    async function processDocument() {
        const textInput = document.getElementById('docContent').value.trim();
        const btn = document.getElementById('btnGenerate');
        const statusDiv = document.getElementById('status');
        const resultArea = document.getElementById('resultArea');

        if (!textInput) {
            alert('Thầy vui lòng nhập nội dung tài liệu ạ!');
            return;
        }

        // Khóa nút bấm và hiện trạng thái
        btn.disabled = true;
        statusDiv.innerText = '⏳ Đang gọi Edge Function (Gemini + Groq) để tạo đề...';
        resultArea.innerHTML = '';

        try {
            // BƯỚC 3.1: Gọi Edge Function để AI xử lý tạo JSON câu hỏi
            const { data, error } = await supabase.functions.invoke('generate-quiz', {
                body: { documentText: textInput }
            });

            if (error) throw error;

            // Giả định Edge Function trả về data.quiz là mảng chứa các câu hỏi
            // (Phụ thuộc vào JSON format mà Groq trả về, ở đây giả sử nó có mảng 'questions')
            const questions = data.quiz.questions || data.quiz; 
            
            statusDiv.innerText = '✅ AI đã tạo xong! Đang lưu vào dữ liệu (bảng question_bank)...';

            // BƯỚC 3.2: Chuẩn bị dữ liệu để lưu vào bảng question_bank
            const recordsToInsert = questions.map(q => ({
                question_text: q.question_text,
                options: q.options,
                correct_answer: q.correct_answer,
                difficulty_level: 'Cơ bản'
            }));

            // BƯỚC 3.3: Lưu trực tiếp vào Supabase từ trình duyệt
            const { error: insertError } = await supabase
                .from('question_bank')
                .insert(recordsToInsert);

            if (insertError) throw insertError;

            statusDiv.innerText = '🎉 Hoàn tất! Đã lưu câu hỏi vào CSDL thành công.';
            statusDiv.style.color = '#27ae60';

            // BƯỚC 3.4: Hiển thị kết quả ra màn hình cho giáo viên xem lại
            questions.forEach((q, index) => {
                const card = document.createElement('div');
                card.className = 'question-card';
                
                // Render các đáp án A, B, C, D
                let optionsHtml = '<ul class="options">';
                if (Array.isArray(q.options)) {
                    q.options.forEach(opt => {
                        optionsHtml += `<li>${opt}</li>`;
                    });
                }
                optionsHtml += '</ul>';

                card.innerHTML = `
                    <b>Câu ${index + 1}: ${q.question_text}</b>
                    ${optionsHtml}
                    <div class="correct">Đáp án đúng: ${q.correct_answer}</div>
                `;
                resultArea.appendChild(card);
            });

        } catch (error) {
            console.error('Lỗi chi tiết:', error);
            statusDiv.innerText = '❌ Có lỗi xảy ra: ' + error.message;
            statusDiv.style.color = '#c0392b';
        } finally {
            // Mở khóa nút bấm
            btn.disabled = false;
        }
    }
</script>

</body>
</html>
