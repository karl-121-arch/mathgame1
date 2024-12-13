<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Math Race Challenge</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #222;
            color: #fff;
            text-align: center;
            margin: 0;
            padding: 0;
        }

        #game-container {
            margin: 50px auto;
            padding: 20px;
            background-color: #333;
            max-width: 400px;
            border-radius: 10px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.3);
        }

        h1 {
            color: #f0a500;
            margin-bottom: 20px;
        }

        #question {
            font-size: 24px;
            margin: 20px 0;
        }

        .btn {
            display: inline-block;
            margin: 10px;
            padding: 10px 20px;
            background-color: #f0a500;
            color: #222;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
        }

        .btn:hover {
            background-color: #d38e00;
        }

        #timer, #score {
            font-size: 18px;
            margin: 10px 0;
        }

        #end-message {
            font-size: 20px;
            margin: 20px 0;
        }
    </style>
</head>
<body>
    <div id="game-container">
        <h1>Math Race Challenge</h1>
        <p id="timer">Time: 30</p>
        <p id="score">Score: 0</p>
        <p id="question">Press "Start" to begin!</p>
        <div>
You sent
<button id="correct-btn" class="btn hidden">Correct</button>
            <button id="incorrect-btn" class="btn hidden">Incorrect</button>
        </div>
        <button id="start-btn" class="btn">Start</button>
        <p id="end-message"></p>
    </div>

    <script>
        // Variables
        let score = 0;
        let timeLeft = 30;
        let interval;
        let currentQuestion;

        const questionElement = document.getElementById("question");
        const correctBtn = document.getElementById("correct-btn");
        const incorrectBtn = document.getElementById("incorrect-btn");
        const startBtn = document.getElementById("start-btn");
        const timerElement = document.getElementById("timer");
        const scoreElement = document.getElementById("score");
        const endMessage = document.getElementById("end-message");

        const questions = [
            { expression: "5 + 3 = 8", correct: true },
            { expression: "7 - 2 = 6", correct: false },
            { expression: "9 × 2 = 18", correct: true },
            { expression: "10 ÷ 5 = 3", correct: false },
            { expression: "12 + 8 = 20", correct: true },
            { expression: "6 × 3 = 19", correct: false },
            { expression: "15 ÷ 3 = 5", correct: true },
            { expression: "8 + 4 = 15", correct: false }
        ];

        // Start Game
        startBtn.addEventListener("click", startGame);

        function startGame() {
            score = 0;
            timeLeft = 30;
            updateScore();
            updateTime();
            endMessage.textContent = "";
            toggleVisibility(startBtn, false);
            toggleVisibility(correctBtn, true);
            toggleVisibility(incorrectBtn, true);
            loadQuestion();
            interval = setInterval(countDown, 1000);
        }

        // Countdown Timer
        function countDown() {
            timeLeft--;
            updateTime();
            if (timeLeft <= 0) {
                endGame();
            }
        }

        // Load a New Question
        function loadQuestion() {
            const randomIndex = Math.floor(Math.random() * questions.length);
            currentQuestion = questions[randomIndex];
            questionElement.textContent = currentQuestion.expression;
        }

        // Handle Correct Answer
        correctBtn.addEventListener("click", () => handleAnswer(true));

        // Handle Incorrect Answer
        incorrectBtn.addEventListener("click", () => handleAnswer(false));

        function handleAnswer(answer) {
            if (answer === currentQuestion.correct) {
                score++;
                updateScore();
            }
            loadQuestion();
        }

        // Update Score
        function updateScore() {
            scoreElement.textContent = Score: ${score};
        }

        // Update Timer
        function updateTime() {
            timerElement.textContent = Time: ${timeLeft};
        }

        // End Game
        function endGame() {
            clearInterval(interval);
            questionElement.textContent = "Game Over!";
            endMessage.textContent = Your final score is ${score}.;
            toggleVisibility(startBtn, true);
            toggleVisibility(correctBtn, false);
            toggleVisibility(incorrectBtn, false);
        }

        // Utility Function: Toggle Visibility
        function toggleVisibility(element, isVisible) {
            element.classList.toggle("hidden", !isVisible);
        }
    </script>
</body>
</html>
