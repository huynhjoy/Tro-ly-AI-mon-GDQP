<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Trợ lý AI môn GDQP&AN</title>
    <!-- Font chữ hiện đại Inter -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    <!-- Thư viện Supabase -->
    <script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2"></script>
    <style>
        :root {
            --primary: #7c3aed; /* Màu tím chủ đạo giống thiết kế */
            --primary-hover: #6d28d9;
            --bg-body: #f5f3ff;
            --bg-card: #ffffff;
            --text-main: #111827;
            --text-muted: #6b7280;
            --border-color: #e5e7eb;
            --bg-input: #f9fafb;
        }

        body {
            font-family: 'Inter', sans-serif;
            background-color: var(--bg-body);
            color: var(--text-main);
            margin: 0;
            padding: 40px 20px;
            display: flex;
            justify-content: center;
        }

        .dashboard-container {
            width: 100%;
            max-width: 900px;
            display: flex;
            flex-direction: column;
            gap: 24px;
        }

        /* HEADER */
        .header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 10px;
        }
        .header h1 { margin: 0; font-size: 24px; font-weight: 700; }
        .header p { margin: 5px 0 0; color: var(--text-muted); font-size: 14px; }
        .btn-template {
            background-color: #111;
            color: #fff;
            padding: 8px 16px;
            border-radius: 8px;
            text-decoration: none;
            font-size: 13px;
            font-weight: 500;
        }

        /* TABS */
        .tabs {
            display: flex;
            background: var(--bg-card);
            padding: 4px;
            border-radius: 12px;
            box-shadow: 0 1px 3px rgba(0,0,0,0.05);
            gap: 4px;
        }
        .tab {
            flex: 1;
            text-align: center;
            padding: 10px;
            font-size: 14px;
            font-weight: 500;
            color: var(--text-muted);
            border-radius: 8px;
            cursor: pointer;
            transition: all 0.2s;
        }
        .tab.active {
            background: var(--bg-body);
            color: var(--primary);
            font-weight: 600;
        }

        /* CARD (Khung trắng) */
        .card {
            background: var(--bg-card);
            border-radius: 16px;
            padding: 24px;
            box-shadow: 0 4px 6px -1px rgba(0,0,0,0.05), 0 2px 4px -1px rgba(0,0,0,0.03);
        }

        /* INPUT AREA */
        .input-header {
            display: flex;
            justify-content: space-between;
            font-size: 14px;
            font-weight: 600;
            margin-bottom: 16px;
        }
        .upload-area {
            border: 2px dashed var(--border-color);
            border-radius: 12px;
            background-color: var(--bg-input);
            padding: 4px;
            transition: border-color 0.2s;
        }
        .upload-area:focus-within { border-color: var(--primary); }
        
        textarea {
            width: 100%;
            height: 180px;
            background: transparent;
            border: none;
            padding: 16px;
            font-size: 14px;
            font-family: inherit;
            resize: vertical;
            box-sizing: border-box;
            outline: none;
            color: var(--text-main);
        }
        textarea::placeholder { color: #9ca3af; text-align: center; line-height: 150px;}

        /* QUIZ SETTINGS */
        .settings-title { font-size: 16px; font-weight: 600; margin-bottom: 16px; margin-top: 8px;}
        .settings-grid {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 16px;
            margin-bottom: 24px;
        }
        .setting-item { display: flex; flex-direction: column; gap: 8px; }
        .setting-item label { font-size: 12px; color: var(--text-muted); font-weight: 500; }
        .setting-item select {
            padding: 10px;
            border: 1px solid var(--border-color);
            border-radius: 8px;
            font-size: 14px;
            background-color: var(--bg-card);
            color: var(--text-main);
            outline: none;
            cursor: pointer;
        }
        
        /* NÚT BẤM */
        .btn-generate {
            width: 100%;
            padding: 14px;
            background-color: var(--primary);
            color: white;
            border: none;
            border-radius: 8px;
            font-size: 15px;
            font-weight: 600;
            cursor: pointer;
            transition: background 0.3s;
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 8px;
        }
        .btn-generate:hover { background-color: var(--primary-hover); }
        .btn-generate:disabled { background-color: #a78bfa; cursor: not-allowed; }

        /* KẾT QUẢ - GIAO DIỆN LÀM BÀI */
        #resultArea { display: none; margin-top: 10px; }
        .quiz-header {
            display: flex;
            justify-content: space-between;
            border-bottom: 1px solid var(--border-color);
            padding-bottom: 16px;
            margin-bottom: 24px;
        }
        .question-block { margin-bottom: 32px; }
        .q-number { font-size: 14px; color: var(--text-muted); font-weight: 500; margin-bottom: 8px; }
        .q-text { font-size: 16px; font-weight: 600; margin-bottom: 16px; display: flex; gap: 12px; }
        .q-icon { color: var(--primary); }
        
        .option {
            display: flex;
            align-items: center;
            padding: 12px 16px;
            border: 1px solid var(--border-color);
            border-radius: 8px;
            margin-bottom: 10px;
            font-size: 14px;
            background: var(--bg-card);
        }
        .option-label {
            background: var(--bg-input);
            border: 1px solid var(--border-color);
            width: 24px;
            height: 24px;
            display: flex;
            align-items: center;
            justify-content: center;
            border-radius: 4px;
            margin-right: 12px;
            font-weight: 600;
            font-size: 12px;
            color: var(--text-muted);
        }
        .correct-answer-box {
            background: #ecfdf5;
            border: 1px solid #10b981;
            color: #047857;
            padding: 10px 16px;
            border-radius: 8px;
            font-size: 13px;
            font-weight: 500;
            margin-top: 12px;
            display: inline-block;
        }

        #statusMsg { text-align: center; font-size: 14px; color: var(--primary); margin-top: 16px; font-weight: 500;}
    </style>
</head>
<body>

<div class="dashboard-container">
    
    <!-- HEADER -->
    <div class="header">
        <div>
            <h1>Generate Quiz</h1>
            <p>Create amazing quizzes from your content with AI-powered generation</p>
        </div>
        <a href="#" class="btn-template">Quản lý Ngân hàng đề</a>
    </div>

    <!-- TABS -->
    <div class="tabs">
        <div class="tab">Tải lên PDF/Word</div>
        <div class="tab">Chọn từ kho tài liệu</div>
        <div class="tab active">Nhập văn bản (Custom Text)</div>
    </div>

    <!-- KHU VỰC NHẬP LIỆU & CÀI ĐẶT -->
    <div class="card">
        <div class="input-header">
            <span>Nội dung bài giảng (GDQP&AN)</span>
            <span style="color: var(--primary); cursor: pointer;">Xóa nội dung</span>
        </div>
        
        <div class="upload-area">
            <textarea id="docContent" placeholder="Dán nội dung văn bản (VD: Kỹ thuật sử dụng lựu đạn) vào đây..."></textarea>
        </div>

        <hr style="border: none; border-top: 1px solid var(--border-color); margin: 24px 0;">

        <div class="settings-title">Quiz Settings</div>
        <div class="settings-grid">
            <div class="setting-item">
                <label>Number of Questions</label>
                <select id="numQuestions">
                    <option value="5">5 Câu hỏi</option>
                    <option value="10">10 Câu hỏi</option>
                    <option value="15">15 Câu hỏi</option>
                </select>
            </div>
            <div class="setting-item">
                <label>Difficulty Level</label>
                <select id="difficulty">
                    <option value="medium">Medium</option>
                    <option value="easy">Easy</option>
                    <option value="hard">Hard</option>
                </select>
            </div>
            <div class="setting-item">
                <label>Time Limit</label>
                <select>
                    <option>15 min</option>
                    <option selected>30 min</option>
                    <option>45 min</option>
                </select>
            </div>
            <div class="setting-item">
                <label>Question Type</label>
                <select>
                    <option>Multiple Choice (MC)</option>
                    <option>True/False</option>
                </select>
            </div>
        </div>

        <button id="btnGenerate" class="btn-generate" onclick="processDocument()">
            <svg width="20" height="20" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M13 10V3L4 14h7v7l9-11h-7z"></path></svg>
            Generate Quiz with AI
        </button>
        <div id="statusMsg"></div>
    </div>

    <!-- KHU VỰC HIỂN THỊ KẾT QUẢ CHUẨN UI -->
    <div id="resultArea" class="card">
        <div class="quiz-header">
            <div>
                <h3 style="margin:0; font-size:18px;">Quiz from AI Generator</h3>
                <p style="margin:5px 0 0; font-size:13px; color:var(--text-muted);" id="quizMeta">Medium • 5 questions</p>
            </div>
            <div style="text-align: right;">
                <p style="margin:0; font-size:12px; color:var(--text-muted);">Trạng thái lưu</p>
                <p style="margin:5px 0 0; font-weight:600; color:#10b981;">Đã lưu vào Supabase</p>
            </div>
        </div>
        
        <div id="questionsContainer"></div>
    </div>

</div>

<script>
    // CẤU HÌNH SUPABASE (Thầy giữ nguyên API Key đã điền trước đó)
    const SUPABASE_URL = 'https://THAY_BANG_URL_CUA_THAY.supabase.co';
    const SUPABASE_ANON_KEY = 'THAY_BANG_ANON_KEY_CUA_THAY';
    const supabase = window.supabase.createClient(SUPABASE_URL, SUPABASE_ANON_KEY);

    const optionLabels = ['A', 'B', 'C', 'D', 'E', 'F'];

    async function processDocument() {
        const textInput = document.getElementById('docContent').value.trim();
        const btn = document.getElementById('btnGenerate');
        const statusMsg = document.getElementById('statusMsg');
        const resultArea = document.getElementById('resultArea');
        const qContainer = document.getElementById('questionsContainer');
        const qMeta = document.getElementById('quizMeta');

        if (!textInput) {
            alert('Thầy vui lòng nhập nội dung tài liệu ạ!');
            return;
        }

        btn.disabled = true;
        btn.innerHTML = `<svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" class="animate-spin"><path d="M21 12a9 9 0 11-18 0 9 9 0 0118 0z"></path></svg> Đang phân tích & Tạo đề...`;
        statusMsg.innerText = 'Đang gọi Edge Function để kết nối Gemini và Groq...';
        resultArea.style.display = 'none';
        qContainer.innerHTML = '';

        try {
            // GỌI EDGE FUNCTION (Đã setup ở bước trước)
            const { data, error } = await supabase.functions.invoke('generate-quiz', {
                body: { documentText: textInput }
            });

            if (error) throw error;
            const questions = data.quiz.questions || data.quiz; 
            statusMsg.innerText = 'Đang đồng bộ dữ liệu vào Ngân hàng câu hỏi...';

            // LƯU VÀO SUPABASE
            const recordsToInsert = questions.map(q => ({
                question_text: q.question_text,
                options: q.options,
                correct_answer: q.correct_answer,
                difficulty_level: document.getElementById('difficulty').value
            }));
            const { error: insertError } = await supabase.from('question_bank').insert(recordsToInsert);
            if (insertError) throw insertError;

            // RENDER GIAO DIỆN KẾT QUẢ
            qMeta.innerText = `${document.getElementById('difficulty').options[document.getElementById('difficulty').selectedIndex].text} • ${questions.length} questions`;
            
            questions.forEach((q, index) => {
                let optionsHtml = '';
                if (Array.isArray(q.options)) {
                    q.options.forEach((opt, i) => {
                        optionsHtml += `
                            <div class="option">
                                <div class="option-label">${optionLabels[i]}</div>
                                <div>${opt}</div>
                            </div>
                        `;
                    });
                }

                qContainer.innerHTML += `
                    <div class="question-block">
                        <div class="q-number">Question ${index + 1} of ${questions.length}</div>
                        <div class="q-text">
                            <span class="q-icon">
                                <svg width="20" height="20" fill="currentColor" viewBox="0 0 20 20"><path fill-rule="evenodd" d="M18 10a8 8 0 11-16 0 8 8 0 0116 0zm-7 4a1 1 0 11-2 0 1 1 0 012 0zm-1-9a1 1 0 00-1 1v4a1 1 0 102 0V6a1 1 0 00-1-1z" clip-rule="evenodd"></path></svg>
                            </span>
                            ${q.question_text}
                        </div>
                        ${optionsHtml}
                        <div class="correct-answer-box">✓ Đáp án đúng: ${q.correct_answer}</div>
                    </div>
                `;
            });

            statusMsg.innerText = '';
            resultArea.style.display = 'block';
            
            // Tự động cuộn xuống kết quả
            resultArea.scrollIntoView({ behavior: 'smooth', block: 'start' });

        } catch (error) {
            console.error(error);
            statusMsg.innerText = '❌ Có lỗi xảy ra: ' + error.message;
            statusMsg.style.color = '#ef4444';
        } finally {
            btn.disabled = false;
            btn.innerHTML = `<svg width="20" height="20" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M13 10V3L4 14h7v7l9-11h-7z"></path></svg> Generate Quiz with AI`;
        }
    }
</script>

</body>
</html>
