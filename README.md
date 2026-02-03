
<html>
<head>
<link href="https://fonts.googleapis.com/css2?family=Noto+Sans+JP:wght@700&display=swap" rel="stylesheet">

<style>
body {
  margin: 0;
  height: 100vh;
  background-color: #ffd1dc;
  overflow: hidden;
  display: flex;
  justify-content: center;
  align-items: center;
}

/* === FALLANDE HJÄRTAN === */
.hearts {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
  z-index: -1; /* 👈 bakom boxen */
}

.heart {
  position: absolute;
  color: #ff8fb1; /* 👈 rosa hjärtan */
  font-size: 20px;
  animation: fall linear infinite;
  opacity: 0.7;
}

@keyframes fall {
  0% {
    transform: translateY(-10vh);
  }
  100% {
    transform: translateY(110vh);
  }
}

/* === HJÄRTEXPLOSION === */
.explosion-heart {
  position: fixed;
  color: #ff4d6d;
  pointer-events: none;
  animation: explode 1s ease-out forwards;
}

@keyframes explode {
  0% {
    transform: translate(0, 0) scale(1);
    opacity: 1;
  }
  100% {
    transform: translate(var(--x), var(--y)) scale(0.5);
    opacity: 0;
  }
}

/* === CENTER BOX === */
.center-box {
  width: 900px;
  min-height: 550px;
  background: white;
  border-radius: 40px;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding-top: 20px;
  z-index: 1; /* 👈 över hjärtana */
}

.center-box img {
  width: 200px;
  height: 200px;
  border-radius: 10px;
  margin-bottom: 20px;
}

.text-box {
  width: 700px;
  padding: 10px;
  font-family: 'Noto Sans JP', sans-serif;
  font-weight: 700;
  font-size: 40px;
  color: #333;
  text-align: center;
}

.button {
  width: 100px;
  height: 60px;
  font-family: 'Noto Sans JP', sans-serif;
  font-weight: 700;
  font-size: 15px;
  border: none;
  border-radius: 50px;
  cursor: pointer;
  display: flex;
  justify-content: center;
  align-items: center;
}

.button-ja {
  background-color: #ff69b4;
  color: white;
}

.button-nej {
  background-color: #dcdcdc;
  color: #333;
  position: relative;
}

.button-container {
  display: flex;
  gap: 180px;
  margin-top: 20px;
}
</style>
</head>

<body>

<!-- FALLANDE HJÄRTAN -->
<div class="hearts" id="hearts"></div>

<div class="center-box">
  <img src="https://thumbs.dreamstime.com/b/print-206284399.jpg">
  <div class="text-box">
    ... vill du bli min valentine?
  </div>
  <div class="button-container">
    <button class="button button-ja">Ja</button>
    <button class="button button-nej">Nej</button>
  </div>
</div>

<script>
/* === FALLANDE HJÄRTAN SCRIPT === */
const heartsContainer = document.getElementById('hearts');
const heartCount = 40;

for (let i = 0; i < heartCount; i++) {
  const heart = document.createElement('div');
  heart.classList.add('heart');
  heart.innerHTML = '❤';

  // X-position: helt slumpad
  heart.style.left = Math.random() * 100 + 'vw';

  // Y-position: flest i mitten, några få uppe
  if (Math.random() < 0.7) {
    // 70% runt mitten
    heart.style.top = 45 + (Math.random() * 20 - 10) + 'vh';
  } else {
    // 30% högre upp
    heart.style.top = Math.random() * 20 + 'vh';
  }

  heart.style.fontSize = Math.random() * 18 + 12 + 'px';

  // Långsammare fall
  const duration = Math.random() * 8 + 14; // 14–22 sek
  heart.style.animationDuration = duration + 's';

  // Starta mitt i animationen
  heart.style.animationDelay = (-Math.random() * duration) + 's';

  heartsContainer.appendChild(heart);
}
</script>




</body>
</html>
