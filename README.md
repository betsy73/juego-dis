# juego-dis
Juego de Disparos (Mate - Ingles)


# idex.html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Juego de Disparos Educativo</title>
  <link rel="stylesheet" href="style.css" />
</head>
<body>
  <div id="game-container">
    <h1>¿Cuánto es <span id="question"></span>?</h1>
    <div id="answers"></div>
    <p>Puntos: <span id="score">0</span> | Vidas: <span id="lives">3</span></p>
  </div>
  <script src="script.js"></script>
</body>
</html>

# style.css
body {
  font-family: Arial, sans-serif;
  background-color: #f0f8ff;
  text-align: center;
  margin: 0;
  padding: 0;
}

#game-container {
  padding: 20px;
}

#answers {
  position: relative;
  height: 300px;
  margin-top: 20px;
  border: 2px solid #333;
  background-color: #e6f7ff;
  overflow: hidden;
}

 absolute;
  padding: 10px 20px;
  background-color: #4caf50;
  color: white;
  border-radius: 5px;
  cursor: pointer;
  transition: top 0.5s;
}

# script.js
const questionEl = document.getElementById("question");
const answersEl = document.getElementById("answers");
const scoreEl = document.getElementById("score");
const livesEl = document.getElementById("lives");

let score = 0;
let lives = 3;

function generateQuestion() {
  const a = Math.floor(Math.random() * 10);
  const b = Math.floor(Math.random() * 10);
  const correct = a + b;
  questionEl.textContent = `${a} + ${b}`;
  generateAnswers(correct);
}

function generateAnswers(correct) {
  answersEl.innerHTML = "";
  const positions = [50, 100, 150, 200];
  const correctIndex = Math.floor(Math.random() * 4);

  for (let i = 0; i < 4; i++) {
    const answer = document.createElement("div");
    answer.classList.add("answer");
    answer.style.left = `${i * 100 + 50}px`;
    answer.style.top = `${positions[Math.floor(Math.random() * positions.length)]}px`;

    const value = i === correctIndex ? correct : correct + Math.floor(Math.random() * 10 - 5);
    answer.textContent = value;

    answer.onclick = () => {
      if (value === correct) {
        score++;
      } else {
        lives--;
      }
      updateStats();
      if (lives > 0) {
        generateQuestion();
      } else {
        alert("¡Juego terminado! Puntuación final: " + score);
        resetGame();
      }
    };

    answersEl.appendChild(answer);
  }
}

function updateStats() {
  scoreEl.textContent = score;
  livesEl.textContent = lives;
}

function resetGame() {
  score = 0;
  lives = 3;
  updateStats();
  generateQuestion();
}

generateQuestion();
