<html>
<head>
<!-- Ladda Noto Sans Japanese från Google Fonts -->
<link href="https://fonts.googleapis.com/css2?family=Noto+Sans+JP:wght@700&display=swap" rel="stylesheet">

<style>
body {
  margin: 0;
  height: 100vh;
  background-color: #ffd1dc; /* pastel pink */
  display: flex;
  justify-content: center;
  align-items: center;
  overflow: hidden; /* förhindrar scroll när knappen flyttar sig */
}

.center-box {
  width: 900px;      
  min-height: 550px;     
  background: white;
  border-radius: 40px;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding-top: 20px;
}

.center-box img {
  width: 200px;         
  height: 200px;        
  border-radius: 10px; 
  margin-bottom: 20px;
}

.text-box {
  width: 700px;
  background-color: #FFFFFF;
  border-radius: 20px;
  padding: 10px;

  font-family: 'Noto Sans JP', sans-serif;
  font-weight: 700;
  font-size: 40px;
  color: #333;

  text-align: center;
  word-wrap: break-word;
}

/* Gemensam knappstil */
.button {
  width: 150px; 
  height: 60px; 
  font-family: 'Noto Sans JP', sans-serif;
  font-weight: 700;
  font-size: 18px;
  border: none;
  outline: none;
  border-radius: 50px;
  cursor: pointer;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  transition: transform 0.2s;
}

.button:hover {
  transform: scale(1.05);
}

/* Färger för knapparna */
.button-ja {
  background-color: #ff69b4; 
  color: white;
}

.button-nej {
  background-color: #b0b0b0; 
  color: #333;
  position: absolute; /* för fri rörelse */
}

/* Container för knappar */
.button-container {
  display: flex;
  gap: 80px; 
  margin-top: 20px;
  align-self: center; 
  position: relative;
}
</style>
</head>

<body>

<div class="center-box">
  <img src="https://thumbs.dreamstime.com/b/print-206284399.jpg" alt="Bild">
  <div class="text-box">
    ... vill du bli min valentine?
  </div>
  <div class="button-container">
    <button class="button button-ja">Ja</button>
    <button class="button button-nej" id="nejButton">Nej</button>
  </div>
</div>

<script>
// Hämta Nej-knappen
const nejButton = document.getElementById('nejButton');
const body = document.body;

// Startposition
let nejX = nejButton.offsetLeft;
let nejY = nejButton.offsetTop;

// Uppdatera knappens position
function updatePosition() {
  nejButton.style.left = nejX + 'px';
  nejButton.style.top = nejY + 'px';
}
updatePosition();

// Lyssna på musrörelser
document.addEventListener('mousemove', e => {
  const mouseX = e.clientX;
  const mouseY = e.clientY;
  
  const rect = nejButton.getBoundingClientRect();
  const buttonCenterX = rect.left + rect.width / 2;
  const buttonCenterY = rect.top + rect.height / 2;
  
  const distance = Math.hypot(mouseX - buttonCenterX, mouseY - buttonCenterY);

  if(distance < 100) { // Om musen är nära
    // Flytta knappen bort från musen
    let offsetX = (buttonCenterX - mouseX) / distance * 120;
    let offsetY = (buttonCenterY - mouseY) / distance * 60;

    nejX += offsetX;
    nejY += offsetY;

    // Håll knappen inom fönstret
    const maxX = window.innerWidth - nejButton.offsetWidth;
    const maxY = window.innerHeight - nejButton.offsetHeight;

    nejX = Math.max(0, Math.min(nejX, maxX));
    nejY = Math.max(0, Math.min(nejY, maxY));

    updatePosition();
  }
});
</script>

</body>
</html>

