
<html lang="sv">
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

:root { --btn-gap: 10px; }

/* === HJÄRTAN === */
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

/* === BOX === */
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

/* === KNAPPAR === */
.button {
  width: 100px;
  height: 60px;
  border-radius: 50px;
  border: none;
  cursor: pointer;
  font-family: 'Noto Sans JP', sans-serif;
}

.button-ja {
  background: #ff69b4;
  color: white;
}
.button-ja:hover { transform: scale(1.12); }

.button-nej {
  background: #dcdcdc;
  position: absolute;
  pointer-events: none;
}

.button-container {
  position: relative;
  margin-top: 20px;
  height: 80px;
}

/* === MODAL === */
.modal-bg {
  position: fixed;
  inset: 0;
  background: rgba(0,0,0,0.4);
  display: none;
  justify-content: center;
  align-items: center;
  z-index: 9999;
}
.modal-box {
  background: #111;
  color: white;
  padding: 20px 30px;
  border-radius: 18px;
  font-family: 'Noto Sans JP', sans-serif;
  min-width: 280px;
  text-align: center;
}
.modal-btn {
  margin-top: 12px;
  padding: 6px 14px;
  border-radius: 16px;
  border: none;
  background: #e6f0ff;
  color: #1b5fd1;
  cursor: pointer;
  font-weight: bold;
}
</style>
</head>

<body>

<div class="hearts" id="hearts"></div>

<div class="center-box">
  <img src="https://thumbs.dreamstime.com/b/print-206284399.jpg" width="200">
  <div class="text-box">... vill du bli min valentine?</div>

  <div class="button-container">
    <button class="button button-ja" id="jaBtn">Ja</button>
    <button class="button button-nej" id="nejBtn">Nej</button>
  </div>
</div>

<div class="modal-bg" id="modal">
  <div class="modal-box">
    <div>OMGG JAAA 💖</div>
    <button class="modal-btn" onclick="closeModal()">OK</button>
  </div>
</div>

<script>
/* === HJÄRTAN === */
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

/* === NEJ-KNAPP: STILLASTÅENDE → FLYR NÄR MUSEN ÄR NÄRA === */
const btn = document.getElementById("nejBtn");

let x = 140;
let y = 0;

btn.style.left = x + "px";
btn.style.top = y + "px";

let lastMouseX = null;
let lastMouseY = null;

const activationRadius = 160;
const speedMultiplier = 1;
const padding = 20;

document.addEventListener("mousemove", e => {
  const rect = btn.getBoundingClientRect();
  const bx = rect.left + rect.width / 2;
  const by = rect.top + rect.height / 2;

  const dx = e.clientX - bx;
  const dy = e.clientY - by;
  const distance = Math.hypot(dx, dy);

  if (distance > activationRadius) {
    lastMouseX = e.clientX;
    lastMouseY = e.clientY;
    return;
  }

  if (lastMouseX === null) {
    lastMouseX = e.clientX;
    lastMouseY = e.clientY;
    return;
  }

  const mdx = e.clientX - lastMouseX;
  const mdy = e.clientY - lastMouseY;

  x -= mdx * speedMultiplier;
  y -= mdy * speedMultiplier;

  lastMouseX = e.clientX;
  lastMouseY = e.clientY;

  keepInside();
  btn.style.left = x + "px";
  btn.style.top = y + "px";
});

function keepInside() {
  const r = btn.getBoundingClientRect();
  const maxX = window.innerWidth - r.width - padding;
  const maxY = window.innerHeight - r.height - padding;

  x = Math.max(padding, Math.min(x, maxX));
  y = Math.max(padding, Math.min(y, maxY));
}

/* === MODAL === */
const modal = document.getElementById("modal");
const jaBtn = document.getElementById("jaBtn");
jaBtn.addEventListener("click", () => modal.style.display = "flex");
function closeModal() { modal.style.display = "none"; }
</script>

</body>
</html>
