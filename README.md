# 22--student-innovation-toys-and-game
flowchart:
bird will start flying >> obstacles will keep on coming >> need to survive by moving the character

#HTML

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Flappy Bird</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <div id="gameArea">
    <div id="bird"></div>
    <div id="pipe"></div>
  </div>
  <div id="gameOverPopup">
    <div id="gameOverText">Game Over</div>
    <button id="retryButton">Retry</button>
  </div>
  <script src="script.js"></script>
</body>
</html>

#CSS

body {
  margin: 0;
  padding: 0;
  overflow: hidden;
}

#gameArea {
  width: 100%;
  height: 600px;
  background-color: skyblue;
  position: relative;
}

#bird {
  width: 50px;
  height: 50px;
  background-color: yellow;
  position: absolute;
  top: 50%;
  left: 50px;
  transform: translateY(-50%);
}

#pipe {
  width: 80px;
  height: 350px;
  background-color: green;
  position: absolute;
  top: 0;
  left: 400px;
}

#gameOverPopup {
  display: none;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background-color: rgba(0, 0, 0, 0.5);
  padding: 20px;
  border-radius: 10px;
  text-align: center;
}

#gameOverText {
  color: white;
  font-size: 24px;
  margin-bottom: 20px;
}

#retryButton {
  background-color: #4CAF50;
  color: white;
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

#JAVA SCRIPT

document.addEventListener('DOMContentLoaded', () => {
  const gameArea = document.getElementById('gameArea');
  const bird = document.getElementById('bird');
  const pipe = document.getElementById('pipe');
  const gameOverPopup = document.getElementById('gameOverPopup');
  const retryButton = document.getElementById('retryButton');

  let birdTop = 220;
  let pipeLeft = 1300;
  let gravity = 3;
  let gameActive = false;

  function jump() {
    if (birdTop > 10) {
      birdTop -= 50;
      bird.style.top = birdTop + 'px';
    }
  }

  function movePipe() {
    if (pipeLeft > -80) {
      pipeLeft -= 5;
      pipe.style.left = pipeLeft + 'px';
      if (pipeLeft < 50 && pipeLeft > -50 && birdTop < 300) {
        endGame();
      }
    } else {
      pipeLeft = 1300;
      pipe.style.left = pipeLeft + 'px';
    }
  }

  function endGame() {
    gameActive = false;
    gameOverPopup.style.display = 'block';
  }

  function resetGame() {
    birdTop = 220;
    pipeLeft = 1300;
    bird.style.top = birdTop + 'px';
    pipe.style.left = pipeLeft + 'px';
    gameActive = true;
    gameOverPopup.style.display = 'none';
  }

  document.addEventListener('keydown', (e) => {
    if (gameActive && e.code === 'Space') {
      jump();
    }
  });

  retryButton.addEventListener('click', () => {
    resetGame();
  });

  gameArea.addEventListener('click', () => {
    if (!gameActive) {
      resetGame();
    }
  });

  setInterval(() => {
    if (gameActive) {
      birdTop += gravity;
      bird.style.top = birdTop + 'px';
      movePipe();
      if (birdTop > 550) {
        endGame();
      }
    }
  }, 50);
});
