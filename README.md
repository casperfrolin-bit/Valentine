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

/* === TEXT === */
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
  transition: transform 0.15s ease-out;
}

/* Ja-knapp */
.button-ja {
  background: #ff69b4;
  color: white;
}

.button-ja:hover {
  transform: scale(1.12);
}

/* Nej-knapp måste vara absolute för att kunna fly */
.button-nej {
  background: #dcdcdc;
  position: absolute;
}

/* === NY: SÄKER KNAPPLAYOUT (så de aldrig krockar) === */
.button-container {
  position: relative;
  width: 500px;            /* bestämmer avståndet mellan dem */
  display: flex;
  justify-content: space-between; /* tvingar isär dem */
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


/* =====================================================
   NEJ-KNAPP SOM FLYR INNANFÖR "RUNDAD SKÄRMKANT"
   (som på din bild)
   ===================================================== */

const btn = document.querySelector(".button-nej");

const dangerRadius = 180;   // hur nära musen den reagerar
const pushStep = 18;        // hur snabbt den flyr
const cornerRadius = 220;   // hur runda hörnen på SKÄRMEN är
const screenPadding = 15;   // liten luft mot kanten

// Startposition = exakt där den redan ligger i layouten
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

  /* --- Flyr från musen --- */
  if (d < dangerRadius) {
    x -= (dx / d) * pushStep;
    y -= (dy / d) * pushStep;
  }

  /* --- Fyrkantiga gränser först --- */
  const minX = screenPadding;
  const minY = screenPadding;
  const maxX = window.innerWidth - r.width - screenPadding;
  const maxY = window.innerHeight - r.height - screenPadding;

  x = Math.max(minX, Math.min(x, maxX));
  y = Math.max(minY, Math.min(y, maxY));

  /* --- RUNDADE HÖRN PÅ SKÄRMKANTEN --- */
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
</script>

</body>
</html>
