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
  inset: 0;
  pointer-events: none;
  z-index: -1;
}

.heart {
  position: absolute;
  color: #ff8fb1;
  animation: fall linear forwards;
  opacity: 0.7;
}

@keyframes fall {
  0% { transform: translateY(-10vh); }
  100% { transform: translateY(110vh); }
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
  z-index: 1;
}

.text-box {
  width: 700px;
  font-family: 'Noto Sans JP', sans-serif;
  font-size: 40px;
  text-align: center;
}

.button {
  width: 100px;
  height: 60px;
  border-radius: 50px;
  border: none;
  cursor: pointer;
  font-family: 'Noto Sans JP', sans-serif;
  transition: transform 0.15s ease-out;
}

/* JA-knapp effekt */
.button-ja {
  background: #ff69b4;
  color: white;
}

.button-ja:hover {
  transform: scale(1.12);
}

/* Nej-knapp måste vara absolute för att röra sig */
.button-nej {
  background: #dcdcdc;
  position: absolute;
}

.button-container {
  display: flex;
  gap: 180px;
  margin-top: 20px;
}
</style>
</head>

<body>

<div class="hearts" id="hearts"></div>

<div class="center-box">
  <img src="https://thumbs.dreamstime.com/b/print-206284399.jpg" width="200">
  <div class="text-box">... vill du bli min valentine?</div>
  <div class="button-container">
    <button class="button button-ja">Ja</button>
    <button class="button button-nej">Nej</button>
  </div>
</div>

<script>
/* ==============================
   OÄNDLIGA HJÄRTAN
   ============================== */
const hearts = document.getElementById("hearts");

function spawnHeart() {
  const h = document.createElement("div");
  h.className = "heart";
  h.textContent = "❤";
  h.style.left = Math.random() * 100 + "vw";
  h.style.fontSize = 12 + Math.random() * 18 + "px";
  h.style.animationDuration = 6 + Math.random() * 6 + "s";
  hearts.appendChild(h);

  setTimeout(() => h.remove(), 12000);
}

for (let i = 0; i < 30; i++) spawnHeart();
setInterval(spawnHeart, 200);


/* ==============================
   NEJ-KNAPP SOM FLYR + VÄGG-PUTT
   (din nya logik – på rätt plats)
   ============================== */

const btn = document.querySelector(".button-nej");

const dangerRadius = 180;
const pushStep = 18;

// behåll exakt startposition
const rectStart = btn.getBoundingClientRect();
let x = rectStart.left;
let y = rectStart.top;

document.addEventListener("mousemove", (e) => {

  const r = btn.getBoundingClientRect();
  const cx = r.left + r.width / 2;
  const cy = r.top + r.height / 2;

  const dx = e.clientX - cx;
  const dy = e.clientY - cy;
  const d = Math.hypot(dx, dy);

  if (d < dangerRadius) {
    x -= (dx / d) * pushStep;
    y -= (dy / d) * pushStep;
  }

  const minX = 0;
  const minY = 0;
  const maxX = window.innerWidth - r.width;
  const maxY = window.innerHeight - r.height;

  // === OSYNLIGA VÄGGAR MED PUTT ===
  if (x <= minX) {
    x = minX;
    y += 25 * (Math.random() > 0.5 ? 1 : -1);
  }

  if (x >= maxX) {
    x = maxX;
    y += 25 * (Math.random() > 0.5 ? 1 : -1);
  }

  if (y <= minY) {
    y = minY;
    x += 25 * (Math.random() > 0.5 ? 1 : -1);
  }

  if (y >= maxY) {
    y = maxY;
    x += 25 * (Math.random() > 0.5 ? 1 : -1);
  }

  // håll inom skärmen
  x = Math.max(minX, Math.min(x, maxX));
  y = Math.max(minY, Math.min(y, maxY));

  btn.style.left = x + "px";
  btn.style.top = y + "px";
});
</script>

</body>
</html>
