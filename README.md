<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>천안호수초등학교 전교학생자치회 회의 발언 타이머 시스템</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            margin: 0;
            background-color: #121212;
            color: #ffffff;
        }
        .timer {
            font-size: 5em;
            color: #ff0000;
            background: #000000;
            padding: 20px;
            border-radius: 10px;
            margin-top: 20px;
        }
        .controls {
            margin-top: 20px;
        }
        button, input {
            margin: 5px;
            padding: 10px 20px;
            font-size: 1em;
            background-color: #333333;
            color: #ffffff;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        button:disabled, input:disabled {
            background-color: #555555;
            cursor: not-allowed;
        }
        button:hover:not(:disabled), input:hover:not(:disabled) {
            background-color: #555555;
        }
        input[type="number"], input[type="text"] {
            width: 80px;
            text-align: center;
        }
    </style>
</head>
<body>
    <h1>천안호수초등학교 전교학생자치회 회의 발언 타이머 시스템</h1>
    <div>
        <button onclick="setTime(1)">1분</button>
        <button onclick="setTime(3)">3분</button>
        <button onclick="setTime(5)">5분</button>
    </div>
    <div class="timer" id="timerDisplay">01:00</div>
    <div class="controls">
        <button id="startButton" onclick="startTimer()">시작</button>
        <button onclick="pauseTimer()">일시 정지</button>
        <button onclick="resetTimer()">초기화</button>
    </div>
    <audio id="endAudio">
        <source src="alarm.mp3" type="audio/mpeg">
        Your browser does not support the audio element.
    </audio>

    <script>
        let timer;
        let totalTime = 60;  // 기본 1분 (60초)
        let remainingTime = totalTime;
        let isActive = false;

        const timerDisplay = document.getElementById('timerDisplay');
        const endAudio = document.getElementById('endAudio');

        function setTime(minutes) {
            totalTime = minutes * 60;
            remainingTime = totalTime;
            updateDisplay(remainingTime);
        }

        function startTimer() {
            if (!isActive) {
                isActive = true;
                timer = setInterval(updateTimer, 1000);
            }
        }

        function pauseTimer() {
            clearInterval(timer);
            isActive = false;
        }

        function resetTimer() {
            clearInterval(timer);
            remainingTime = totalTime;
            isActive = false;
            updateDisplay(remainingTime);
        }

        function updateTimer() {
            if (remainingTime > 0) {
                remainingTime--;
                updateDisplay(remainingTime);
            } else {
                clearInterval(timer);
                isActive = false;
                endAudio.play();
                alert('발언 시간이 모두 끝났습니다.');
            }
        }

        function updateDisplay(time) {
            const minutes = Math.floor(time / 60);
            const seconds = time % 60;
            timerDisplay.textContent = `${minutes}분 ${seconds}초`;
        }

        document.addEventListener('DOMContentLoaded', () => {
            updateDisplay(totalTime);
        });
    </script>
</body>
</html>
