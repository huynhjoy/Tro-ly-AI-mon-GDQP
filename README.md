<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>JOY EDU - Trợ lý AI GDQP&AN</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap" rel="stylesheet">
    <script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2"></script>
    <style>
        :root {
            --bg: #f3f4f6; --sf: #ffffff; --tx: #111827; --mu: #6b7280; 
            --ln: #e5e7eb; --pr: #10b981; --pr-hover: #059669;
            --sh: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
        }
        body { margin: 0; background: var(--bg); color: var(--tx); font-family: 'Inter', sans-serif; padding: 40px 20px; }
        .container { max-width: 800px; margin: 0 auto; }
        .hero { background: linear-gradient(135deg, #064e3b 0%, #10b981 100%); color: #fff; padding: 24px; border-radius: 16px; margin-bottom: 24px; box-shadow: var(--sh); }
        .hero h1 { margin: 0; font-size: 1.8rem; font-weight: 800; }
        .card { background: var(--sf); border: 1px solid var(--ln); border-radius: 16px; padding: 24px; margin-bottom: 24px; box-shadow: var(--sh); }
        textarea { width: 100%; height: 180px; padding: 16px; border: 2px dashed var(--ln); border-radius: 12px; background: #f9fafb; font-family: inherit; font-size: 15px; box-sizing: border-box; resize: vertical; outline: none; transition: 0.2s; margin-bottom: 16px; }
        textarea:focus { border-color: var(--pr); background: var(--sf); }
        button { width: 100%; padding: 14px; background: var(--pr); color: #fff; font-size: 16px; font-weight: 600; border: none; border-radius: 12px; cursor: pointer; transition: 0.2s; box-shadow: 0 2px 4px rgba(16, 185, 129, 0.2); }
        button:hover { background: var(--pr-hover); transform: translateY(-1px); }
        button:disabled { background: #9ca3af; cursor: not-allowed; transform: none; }
        #statusMsg { text-align: center; color: var(--pr); font-weight: 600; margin-top: 16px; font-size: 14px; }
        .question-box { border: 1px solid var(--ln); border-radius: 12px; padding: 16px; margin-bottom: 16px; background: #f8fafc; border-left: 4px solid var(--pr); }
        .opt-row { background: var(--sf); border: 1px solid var(--ln); padding: 10px 16px; margin: 8px 0; border-radius: 8px; font-size: 14px; }
        .ans-true { color: #047857; background: #d1fae5; font-weight: 600; margin-top: 12px; padding: 8px 12px; border-radius: 6px; display: inline-block; font-size: 13px; }
    </style>
</head>
<body>

<div class="container">
    <div class="hero">
        <h1>JOY EDU - Backend Flow</h1>
        <p style="margin: 5px 0 0; opacity: 0.9;">Gemini ➔ Supabase ➔ Groq ➔ Supabase</p>
    </div>

    <div class="card">
        <h2 style="margin-top:0; font-size: 1.2rem;">Nhập nội dung SGK GDQP&AN</h2>
        <textarea id="docContent" placeholder="Dán văn bản bài học vào đây để hệ thống tự động trích xuất JSON và sinh đề thi..."></textarea>
        <button id="btnGenerate" onclick="processBackendFlow()">🚀 Kích hoạt Luồng Xử Lý AI</button>
        <div id="statusMsg"></div>
    </div>

    <div id="resultArea" class="card" style="display: none;">
        <h2 style="margin-top:0; font-size: 1.2rem; color: var(--pr);">Kết quả Trắc nghiệm từ Groq</h2>
        <p style="font-size: 13px; color: var(--mu); margin-top: -5px; margin-bottom: 20px;">Toàn bộ dữ liệu đã được lưu ngầm vào Supabase.</p>
        <div id="quizContainer"></div>
    </div>
</div>

<script>
    // Chỉ cần điền URL và ANON KEY để gọi Edge Function
    const CFG = {
        url: 'https://THAY_URL_CUA_THAY.supabase.co',
        key: 'THAY_ANON_KEY_CUA_THAY'
    };
    const supabase = window.supabase.createClient(CFG.url, CFG.key);

    async function processBackendFlow() {
        const text = document.getElementById('docContent').value.trim();
        const btn = document.getElementById('btnGenerate');
        const msg = document.getElementById('statusMsg');
        const resultArea = document.getElementById('resultArea');
        const container = document.getElementById('quizContainer');

        if (!text) return alert('Vui lòng nhập nội dung bài học!');

        btn.disabled = true;
        btn.innerText = '⏳ Hệ thống đang xử lý qua 4 bước Backend...';
        msg.innerText = 'Đang gọi hàm joy-edu-api trên Supabase...';
        resultArea.style.display = 'none';
        container.innerHTML = '';

        try {
            // Chỉ gọi API 1 lần duy nhất, Backend sẽ tự lo việc chạy Gemini -> DB -> Groq -> DB
            const { data, error } = await supabase.functions.invoke('joy-edu-api', {
                body: { documentText: text }
            });

            if (error) throw error;
            if (!data.success) throw new Error(data.error);

            msg.innerText = '✅ Quá trình khép kín hoàn tất thành công!';
            
            const questions = data.quiz.questions || data.quiz;
            const labels = ['A', 'B', 'C', 'D'];

            questions.forEach((q, idx) => {
                let optsHTML = '';
                if(Array.isArray(q.options)) {
                    q.options.forEach((opt, i) => {
                        optsHTML += `<div class="opt-row"><b>${labels[i]}.</b> ${opt}</div>`;
                    });
                }
                container.innerHTML += `
                    <div class="question-box">
                        <b style="font-size:15px;">Câu ${idx + 1}: ${q.q || q.question}</b>
                        <div style="margin-top: 12px;">${optsHTML}</div>
                        <div class="ans-true">✓ Đáp án đúng: ${q.a || q.answer}</div>
                    </div>
                `;
            });
            
            resultArea.style.display = 'block';

        } catch (err) {
            console.error(err);
            msg.style.color = 'var(--no)';
            msg.innerText = '❌ Lỗi hệ thống: ' + (err.message || 'Kiểm tra log Supabase');
        } finally {
            btn.disabled = false;
            btn.innerText = '🚀 Kích hoạt Luồng Xử Lý AI';
        }
    }
</script>

</body>
</html>
