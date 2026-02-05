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

/* === JA-KNAPP EFFEKT === */
.button-ja {
  background: #ff69b4;
  color: white;
}

.button-ja:hover {
  transform: scale(1.12);
}

/* === NEJ-KNAPP (MÅSTE VARA ABSOLUTE FÖR ATT KUNNA RÖRA SIG) === */
.button-nej {
  background: #dcdcdc;
  position: absolute;
}

/* container – bara layout (rörs inte av JS) */
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
   1 + 2) OMÖJLIG NEJ-KNAPP
   MED MJUKA RUNDADE KANTER
   ============================== */

const btn = document.querySelector(".button-nej");
const dangerRadius = 160;
const cornerRadius = 140;
const screenPadding = 10;

// Sätt startposition exakt där knappen redan ligger
const rectStart = btn.getBoundingClientRect();
let x = rectStart.left;
let y = rectStart.top;

let lastMouse = { x: null, y: null };

document.addEventListener("mousemove", (e) => {

  const r = btn.getBoundingClientRect();
  const cx = r.left + r.width / 2;
  const cy = r.top + r.height / 2;

  const dx = e.clientX - cx;
  const dy = e.clientY - cy;
  const d = Math.hypot(dx, dy);

  // === Flyr i SAMMA FART som musen när du är nära ===
  if (d < dangerRadius) {
    if (lastMouse.x !== null) {
      const mx = e.clientX - lastMouse.x;
      const my = e.clientY - lastMouse.y;

      x -= mx;
      y -= my;
    }
  }

  lastMouse = { x: e.clientX, y: e.clientY };

  // === Fyrkantiga gränser (men med mjuka hörn) ===
  const minX = screenPadding;
  const minY = screenPadding;
  const maxX = window.innerWidth - r.width - screenPadding;
  const maxY = window.innerHeight - r.height - screenPadding;

  // först vanlig clamp
  x = Math.max(minX, Math.min(x, maxX));
  y = Math.max(minY, Math.min(y, maxY));

  // Hörn som cirklar (så den inte fastnar)
  const corners = [
    { cx: minX + cornerRadius, cy: minY + cornerRadius },
    { cx: maxX - cornerRadius, cy: minY + cornerRadius },
    { cx: minX + cornerRadius, cy: maxY - cornerRadius },
    { cx: maxX - cornerRadius, cy: maxY - cornerRadius }
  ];

  const bx = x + r.width / 2;
  const by = y + r.height / 2;

  for (const c of corners) {
    const vx = bx - c.cx;
    const vy = by - c.cy;
    const dist = Math.hypot(vx, vy);

    if (dist < cornerRadius) {
      const scale = cornerRadius / (dist || 0.1);
      x = c.cx + vx * scale - r.width / 2;
      y = c.cy + vy * scale - r.height / 2;
    }
  }

  btn.style.left = x + "px";
  btn.style.top = y + "px";
});


/* ==============================
   3) OÄNDLIGA HJÄRTAN
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

  // ta bort när den ramlat klart
  setTimeout(() => h.remove(), 12000);
}

// start med några
for (let i = 0; i < 30; i++) spawnHeart();

// sedan NYA hela tiden
setInterval(spawnHeart, 200);

</script>

</body>
</html>
