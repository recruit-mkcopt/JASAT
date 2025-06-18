<!DOCTYPE html>
<html lang="zh-Hant">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>五專聯合免試入學成績試算</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        /* Inter font for better readability */
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap');
        body {
            font-family: 'Inter', sans-serif;
            background-color: #f0f2f5; /* Light grey background */
            color: #333;
        }
        .container {
            max-width: 800px;
            margin: 2rem auto;
            padding: 2rem;
            background-color: #ffffff;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            border-radius: 12px;
        }
        input[type="number"], select {
            width: 100%;
            padding: 0.75rem;
            border: 1px solid #d1d5db; /* Light grey border */
            border-radius: 8px;
            margin-top: 0.5rem;
            font-size: 1rem;
            transition: border-color 0.2s;
        }
        input[type="number"]:focus, select:focus {
            outline: none;
            border-color: #6366f1; /* Indigo focus */
            box-shadow: 0 0 0 3px rgba(99, 102, 241, 0.2);
        }
        .score-item label {
            font-weight: 500;
            color: #1f2937; /* Darker text for labels */
        }
        .score-item p.text-sm {
            color: #6b7280; /* Grey text for descriptions */
            margin-top: 0.25rem;
        }
        button {
            background: linear-gradient(to right, #6366f1, #8b5cf6); /* Indigo to Purple gradient */
            color: white;
            padding: 1rem 1.5rem;
            border-radius: 8px;
            font-weight: 600;
            cursor: pointer;
            transition: transform 0.2s ease-in-out, box-shadow 0.2s ease-in-out;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            width: 100%;
        }
        button:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 8px rgba(0, 0, 0, 0.15);
        }
        .result-box {
            background-color: #eff6ff; /* Light blue background for results */
            border: 1px solid #bfdbfe; /* Blue border */
            border-radius: 8px;
            padding: 1.5rem;
            margin-top: 2rem;
        }
        .result-box h3 {
            font-size: 1.25rem;
            font-weight: 600;
            color: #1e3a8a; /* Dark blue for result heading */
            margin-bottom: 1rem;
        }
        .result-box p {
            margin-bottom: 0.5rem;
        }
        .total-score {
            font-size: 1.75rem;
            font-weight: 700;
            color: #c026d3; /* Vibrant purple for total score */
            text-align: center;
            margin-top: 1.5rem;
        }
        .error-message {
            color: #ef4444; /* Red for error messages */
            font-size: 0.875rem;
            margin-top: 0.5rem;
        }
    </style>
</head>
<body class="p-4">
    <div class="container">
        <h1 class="text-3xl font-bold text-center mb-6 text-gray-800">五專聯合免試入學成績試算</h1>
        <p class="text-center text-gray-600 mb-8">請輸入您的相關資訊，本工具將自動為您估算聯合免試入學總成績。此試算結果僅供參考，實際成績請依招生委員會公告為準。<br><strong>馬偕視光招生小組 設計製作</strong></p>

        <div class="mb-8 p-6 bg-gray-50 rounded-lg shadow-sm">
            <h2 class="text-2xl font-semibold mb-6 text-gray-700">成績輸入</h2>
            <p class="mb-6 text-gray-600">請輸入您各項成績或勾選符合的項目，並確保分數在指定範圍內。</p>

            <!-- 1. 多元學習表現 -->
            <div class="mb-5 score-item">
                <label for="multicultural_learning" class="block text-lg mb-1">1. 多元學習表現 (滿分16分)</label>
                <input type="number" id="multicultural_learning" placeholder="請輸入得分" min="0" max="16" class="mt-1">
                <p class="text-sm text-gray-500 mt-1">此為未加權分數，請填寫學校給予的原始分數。</p>
                <div id="multicultural_learning_error" class="error-message hidden"></div>
            </div>

            <!-- 2. 技藝優良 -->
            <div class="mb-5 score-item">
                <label for="skill_excellence" class="block text-lg mb-1">2. 技藝優良 (滿分3分)</label>
                <input type="number" id="skill_excellence" placeholder="請輸入得分" min="0" max="3" class="mt-1">
                <p class="text-sm text-gray-500 mt-1">此為未加權分數，請填寫學校給予的原始分數。</p>
                <div id="skill_excellence_error" class="error-message hidden"></div>
            </div>

            <!-- 3. 弱勢身分 -->
            <div class="mb-5 score-item">
                <label class="block text-lg mb-2">3. 弱勢身分 (滿分2分)</label>
                <div class="flex items-center space-x-4">
                    <label class="inline-flex items-center">
                        <input type="radio" name="disadvantaged_status" value="yes" class="form-radio text-indigo-600 rounded-full h-5 w-5">
                        <span class="ml-2 text-gray-700">是</span>
                    </label>
                    <label class="inline-flex items-center">
                        <input type="radio" name="disadvantaged_status" value="no" class="form-radio text-indigo-600 rounded-full h-5 w-5" checked>
                        <span class="ml-2 text-gray-700">否</span>
                    </label>
                </div>
                <p class="text-sm text-gray-500 mt-1">符合低收入戶、中低收入戶、直系血親尊親屬支領失業給付子女或特殊境遇家庭子女，任何一種身分者得2分。</p>
            </div>

            <!-- 4. 均衡學習 -->
            <div class="mb-5 score-item">
                <label for="balanced_learning" class="block text-lg mb-1">4. 均衡學習 (滿分6分)</label>
                <input type="number" id="balanced_learning" placeholder="請輸入得分" min="0" max="6" class="mt-1">
                <p class="text-sm text-gray-500 mt-1">此為未加權分數，請填寫學校給予的原始分數。</p>
                <div id="balanced_learning_error" class="error-message hidden"></div>
            </div>

            <!-- 5. 適性輔導 -->
            <div class="mb-5 score-item">
                <label for="adaptive_counseling" class="block text-lg mb-1">5. 適性輔導 (滿分3分)</label>
                <input type="number" id="adaptive_counseling" placeholder="請輸入得分" min="0" max="3" class="mt-1">
                <p class="text-sm text-gray-500 mt-1">此為未加權分數，請填寫學校給予的原始分數。</p>
                <div id="adaptive_counseling_error" class="error-message hidden"></div>
            </div>

            <!-- 6. 會考成績 -->
            <div class="mb-5 score-item">
                <label class="block text-lg mb-2">6. 會考成績 (滿分15分)</label>
                <p class="text-sm text-gray-500 mb-2">請選擇您各科的等級：(A等3分, B等2分, C等1分)</p>
                <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                    <div>
                        <label for="exam_chinese" class="block text-md mb-1">國文：</label>
                        <select id="exam_chinese" class="mt-1">
                            <option value="0">請選擇</option>
                            <option value="3">A</option>
                            <option value="2">B</option>
                            <option value="1">C</option>
                        </select>
                    </div>
                    <div>
                        <label for="exam_math" class="block text-md mb-1">數學：</label>
                        <select id="exam_math" class="mt-1">
                            <option value="0">請選擇</option>
                            <option value="3">A</option>
                            <option value="2">B</option>
                            <option value="1">C</option>
                        </select>
                    </div>
                    <div>
                        <label for="exam_english" class="block text-md mb-1">英文：</label>
                        <select id="exam_english" class="mt-1">
                            <option value="0">請選擇</option>
                            <option value="3">A</option>
                            <option value="2">B</option>
                            <option value="1">C</option>
                        </select>
                    </div>
                    <div>
                        <label for="exam_science" class="block text-md mb-1">自然：</label>
                        <select id="exam_science" class="mt-1">
                            <option value="0">請選擇</option>
                            <option value="3">A</option>
                            <option value="2">B</option>
                            <option value="1">C</option>
                        </select>
                    </div>
                    <div>
                        <label for="exam_social" class="block text-md mb-1">社會：</label>
                        <select id="exam_social" class="mt-1">
                            <option value="0">請選擇</option>
                            <option value="3">A</option>
                            <option value="2">B</option>
                            <option value="1">C</option>
                        </select>
                    </div>
                </div>
                <div id="exam_score_error" class="error-message hidden"></div>
            </div>

            <!-- 7. 英文檢定 -->
            <div class="mb-5 score-item">
                <label for="english_test" class="block text-lg mb-1">7. 英文檢定 (滿分5分)</label>
                <input type="number" id="english_test" placeholder="請輸入得分" min="0" max="5" class="mt-1">
                <p class="text-sm text-gray-500 mt-1">此為未加權分數，請填寫通過檢定可得的原始分數。</p>
                <div id="english_test_error" class="error-message hidden"></div>
            </div>

            <button id="calculate_button" class="mt-8">計算總成績</button>
        </div>

        <div id="result_display" class="result-box hidden">
            <h3 class="mb-4">您的各項加權分數：</h3>
            <p><strong>多元學習表現：</strong> <span id="res_multicultural_learning">0</span> 分 (未加權得分 x 1.5)</p>
            <p><strong>技藝優良：</strong> <span id="res_skill_excellence">0</span> 分 (未加權得分 x 1)</p>
            <p><strong>弱勢身分：</strong> <span id="res_disadvantaged_status">0</span> 分 (未加權得分 x 1)</p>
            <p><strong>均衡學習：</strong> <span id="res_balanced_learning">0</span> 分 (未加權得分 x 1)</p>
            <p><strong>適性輔導：</strong> <span id="res_adaptive_counseling">0</span> 分 (未加權得分 x 1)</p>
            <p><strong>會考成績：</strong> <span id="res_exam_score">0</span> 分 (未加權得分 x 1.4)</p>
            <p><strong>英文檢定：</strong> <span id="res_english_test">0</span> 分 (未加權得分 x 1)</p>
            <hr class="my-4 border-t-2 border-blue-200">
            <p class="total-score">您的聯合免試入學總成績估計為：<span id="final_total_score">0</span> 分 (滿分64分)</p>
        </div>

        <div class="mt-8 p-4 bg-yellow-50 border border-yellow-200 rounded-lg text-yellow-800">
            <h3 class="font-semibold text-lg mb-2">重要提示</h3>
            <p>本試算工具的結果僅供初步參考，實際錄取標準與各項細節請務必參閱當年度<a href="https://www.techadmi.edu.tw/tw/" target="_blank" class="text-blue-600 hover:underline">五專聯合免試入學招生簡章</a>。</p>
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
            const calculateButton = document.getElementById('calculate_button');
            const resultDisplay = document.getElementById('result_display');

            // Function to validate numerical input and display error
            function validateInput(inputId, maxScore) {
                const inputElement = document.getElementById(inputId);
                const errorElement = document.getElementById(`${inputId}_error`);
                let value = parseFloat(inputElement.value);

                if (isNaN(value) || value < 0 || value > maxScore) {
                    errorElement.textContent = `請輸入介於 0 到 ${maxScore} 之間的有效數字。`;
                    errorElement.classList.remove('hidden');
                    return false;
                } else {
                    errorElement.classList.add('hidden');
                    return value;
                }
            }

            // Function to validate exam scores
            function validateExamScores() {
                const examSubjects = ['chinese', 'math', 'english', 'science', 'social'];
                let allSelected = true;
                examSubjects.forEach(subject => {
                    const selectElement = document.getElementById(`exam_${subject}`);
                    if (selectElement.value === '0') {
                        allSelected = false;
                    }
                });

                const errorElement = document.getElementById('exam_score_error');
                if (!allSelected) {
                    errorElement.textContent = '請選擇所有會考科目的成績等級。';
                    errorElement.classList.remove('hidden');
                    return false;
                } else {
                    errorElement.classList.add('hidden');
                    return true;
                }
            }

            calculateButton.addEventListener('click', () => {
                let totalIsValid = true;

                // 1. 多元學習表現
                let multiculturalLearning = validateInput('multicultural_learning', 16);
                if (multiculturalLearning === false) totalIsValid = false;

                // 2. 技藝優良
                let skillExcellence = validateInput('skill_excellence', 3);
                if (skillExcellence === false) totalIsValid = false;

                // 3. 弱勢身分
                const disadvantagedStatusRadio = document.querySelector('input[name="disadvantaged_status"]:checked');
                // Updated score for disadvantaged status
                let disadvantagedStatus = (disadvantagedStatusRadio && disadvantagedStatusRadio.value === 'yes') ? 2 : 0;

                // 4. 均衡學習
                let balancedLearning = validateInput('balanced_learning', 6);
                if (balancedLearning === false) totalIsValid = false;

                // 5. 適性輔導
                let adaptiveCounseling = validateInput('adaptive_counseling', 3);
                if (adaptiveCounseling === false) totalIsValid = false;

                // 6. 會考成績
                let examScore = 0;
                if (validateExamScores()) {
                    const examSubjects = ['chinese', 'math', 'english', 'science', 'social'];
                    examSubjects.forEach(subject => {
                        examScore += parseInt(document.getElementById(`exam_${subject}`).value);
                    });
                } else {
                    totalIsValid = false;
                }

                // 7. 英文檢定
                let englishTest = validateInput('english_test', 5);
                if (englishTest === false) totalIsValid = false;

                // If any input is invalid, stop calculation and show message
                if (!totalIsValid) {
                    resultDisplay.classList.add('hidden');
                    // Optionally, you can add a general error message here if needed
                    return;
                }

                // --- 計算加權分數 ---
                const weightedScores = {};
                weightedScores.multiculturalLearning = multiculturalLearning * 1.5;
                weightedScores.skillExcellence = skillExcellence * 1;
                weightedScores.disadvantagedStatus = disadvantagedStatus * 1; // Weighted by 1 as per instruction
                weightedScores.balancedLearning = balancedLearning * 1;
                weightedScores.adaptiveCounseling = adaptiveCounseling * 1;
                weightedScores.examScore = examScore * 1.4;
                weightedScores.englishTest = englishTest * 1;

                // --- 計算總分 ---
                let finalTotalScore = 0;
                for (const key in weightedScores) {
                    finalTotalScore += weightedScores[key];
                }
                // 確保總分不超過64，雖然根據您的設定應該不會超過
                finalTotalScore = Math.min(finalTotalScore, 64);

                // --- 顯示結果 ---
                document.getElementById('res_multicultural_learning').textContent = weightedScores.multiculturalLearning.toFixed(2);
                document.getElementById('res_skill_excellence').textContent = weightedScores.skillExcellence.toFixed(2);
                document.getElementById('res_disadvantaged_status').textContent = weightedScores.disadvantagedStatus.toFixed(2);
                document.getElementById('res_balanced_learning').textContent = weightedScores.balancedLearning.toFixed(2);
                document.getElementById('res_adaptive_counseling').textContent = weightedScores.adaptiveCounseling.toFixed(2);
                document.getElementById('res_exam_score').textContent = weightedScores.examScore.toFixed(2);
                document.getElementById('res_english_test').textContent = weightedScores.englishTest.toFixed(2);
                document.getElementById('final_total_score').textContent = finalTotalScore.toFixed(2);

                resultDisplay.classList.remove('hidden');
            });
        });
    </script>
</body>
</html>
