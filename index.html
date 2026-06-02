<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>App Chấm Điểm Phát Âm Tiếng Trung</title>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: #f4f7f6;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
        }
        .container {
            background-color: #fff;
            padding: 30px;
            border-radius: 12px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
            text-align: center;
            max-width: 500px;
            width: 100%;
        }
        h1 { color: #333; font-size: 24px; }
        .sentence-box {
            background-color: #eef2f7;
            padding: 15px;
            border-radius: 8px;
            margin: 20px 0;
            font-size: 22px;
            font-weight: bold;
            color: #2c3e50;
        }
        .pinyin {
            font-size: 16px;
            color: #7f8c8d;
            font-weight: normal;
            margin-top: 5px;
        }
        button {
            background-color: #3498db;
            color: white;
            border: none;
            padding: 12px 25px;
            font-size: 16px;
            border-radius: 25px;
            cursor: pointer;
            transition: background 0.3s;
        }
        button:hover { background-color: #2980b9; }
        button:disabled { background-color: #bdc3c7; }
        .recording { background-color: #e74c3c !important; }
        #result {
            margin-top: 20px;
            font-size: 18px;
            font-weight: bold;
        }
        .score { font-size: 28px; color: #2ecc71; margin-top: 10px; }
    </style>
</head>
<body>

<div class="container">
    <h1>Phát Âm Tiếng Trung Chuẩn</h1>
    <p>Hãy đọc câu dưới đây:</p>
    
    <div class="sentence-box">
        <span id="target-text">你好</span>
        <div class="pinyin" id="target-pinyin">Nǐ hǎo</div>
    </div>

    <button id="record-btn">Bắt đầu nói</button>
    
    <div id="status" style="margin-top: 15px; color: #7f8c8d;"></div>
    
    <div id="result">
        <p>Bạn đã nói: <span id="user-speech" style="color: #34495e;">...</span></p>
        <div class="score" id="score-display"></div>
    </div>
</div>

<script>
    // THAY API KEY CỦA BẠN VÀO ĐÂY
    const GOOGLE_API_KEY = "YOUR_GOOGLE_CLOUD_API_KEY"; 

    const targetText = document.getElementById('target-text').innerText;
    const recordBtn = document.getElementById('record-btn');
    const statusText = document.getElementById('status');
    const userSpeechText = document.getElementById('user-speech');
    const scoreDisplay = document.getElementById('score-display');

    let mediaRecorder;
    let audioChunks = [];
    let isRecording = false;

    recordBtn.addEventListener('click', async () => {
        if (!isRecording) {
            // Bắt đầu ghi âm
            audioChunks = [];
            const stream = await navigator.mediaDevices.getUserMedia({ audio: true });
            mediaRecorder = new MediaRecorder(stream);
            
            mediaRecorder.ondataavailable = event => {
                audioChunks.push(event.data);
            };

            mediaRecorder.onstop = async () => {
                const audioBlob = new Blob(audioChunks, { type: 'audio/webm' });
                statusText.innerText = "Đang phân tích phát âm...";
                sendToGoogleSpeech(audioBlob);
            };

            mediaRecorder.start();
            isRecording = true;
            recordBtn.innerText = "Dừng nói & Chấm điểm";
            recordBtn.classList.add('recording');
            statusText.innerText = "Đang lắng nghe... Hãy nói đi!";
        } else {
            // Dừng ghi âm
            mediaRecorder.stop();
            isRecording = false;
            recordBtn.innerText = "Bắt đầu nói";
            recordBtn.classList.remove('recording');
        }
    });

    // Hàm chuyển đổi Blob âm thanh sang Base64 và gửi lên Google API
    async function sendToGoogleSpeech(blob) {
        const reader = new FileReader();
        reader.readAsDataURL(blob);
        reader.onloadend = async () => {
            const base64Audio = reader.result.split(',')[1]; // Lấy phần dữ liệu mã hóa

            const requestBody = {
                config: {
                    encoding: "WEBM_OPUS",
                    sampleRateHertz: 48000,
                    languageCode: "cmn-Hans-CN" // Tiếng Trung Phổ Thông
                },
                audio: {
                    content: base64Audio
                }
            };

            try {
                const response = await fetch(`https://speech.googleapis.com/v1/speech:recognize?key=${GOOGLE_API_KEY}`, {
                    method: "POST",
                    headers: { "Content-Type": "application/json" },
                    body: JSON.stringify(requestBody)
                });

                const data = await response.json();
                
                if (data.results && data.results.length > 0) {
                    const transcript = data.results[0].alternatives[0].transcript;
                    userSpeechText.innerText = transcript;
                    calculateScore(transcript, targetText);
                } else {
                    userSpeechText.innerText = "(Không nhận diện được âm thanh)";
                    scoreDisplay.innerText = "0 Điểm";
                    statusText.innerText = "Thử lại nhé!";
                }
            } catch (error) {
                console.error("Lỗi kết nối API:", error);
                statusText.innerText = "Có lỗi xảy ra khi kết nối API.";
            }
        };
    }

    // Hàm so sánh chuỗi đơn giản để chấm điểm
    function calculateScore(userStr, targetStr) {
        // Xóa dấu câu khoảng cách để so sánh chính xác ký tự tự nhiên
        const cleanUser = userStr.replace(/[.,\/#!$%\^&\*;:{}=\-_`~()?\s]/g,"");
        const cleanTarget = targetStr.replace(/[.,\/#!$%\^&\*;:{}=\-_`~()?\s]/g,"");

        let matchCount = 0;
        for (let char of cleanUser) {
            if (cleanTarget.includes(char)) {
                matchCount++;
            }
        }

        // Tính tỷ lệ phần trăm chính xác
        let score = Math.round((matchCount / cleanTarget.length) * 100);
        if (score > 100) score = 100; // Giới hạn max 100

        scoreDisplay.innerText = `${score} / 100 Điểm`;
        statusText.innerText = score >= 80 ? "Tuyệt vời! Phát âm rất chuẩn." : "Khá tốt, hãy luyện tập thêm!";
    }
</script>

</body>
</html>
