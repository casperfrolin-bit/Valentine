<html>
<head>
<!-- Ladda Noto Sans Japanese från Google Fonts -->
<link href="https://fonts.googleapis.com/css2?family=Noto+Sans+JP:wght@700&display=swap" rel="stylesheet">

<style>
body {
  margin: 0;
  height: 100vh;
  background-color: #ffd1dc;
  overflow: hidden; /* förhindrar scroll */
  display: flex;
  justify-content: center;
  align-items: center;
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

.button {
  font-family: 'Noto Sans JP', sans-serif;
  font-weight: 700;
  border: none;
  outline: none;
  border-radius: 50px;
  cursor: pointer;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  transition: transform 0.05s;
}

.button-ja {
  width: 150px;
  height: 60px;
  font-size: 18px;
  background-color: #ff69b4;
  color: white;
  margin-top: 20px;
}

.button-nej {
  width: 150px;
  height: 60px;
  font-size: 18px;
  background-color: #b0b0b0;
  color: #333;
  position: absolute;
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
const nejButton = document.getElementById('nejButton');

// Startposition: mitt på skärmen
let posX = window.innerWidth / 2;
let posY = window.innerHeight / 2;
nejButton.style.left = posX + 'px';
nejButton.style.top = posY + 'px';

document.addEventListener('mousemove', e => {
  const mouseX = e.clientX;
  const mouseY = e.clientY;

  const rect = nejButton.getBoundingClientRect();
  const buttonCenterX = rect.left + rect.width / 2;
  const buttonCenterY = rect.top + rect.height / 2;

  const distance = Math.hypot(mouseX - buttonCenterX, mouseY - buttonCenterY);

  if(distance < 150) { // när musen är nära
    // Flytta fritt i alla riktningar
    const dx = (buttonCenterX - mouseX) / distance * (50 + Math.random() * 150);
    const dy = (buttonCenterY - mouseY) / distance * (30 + Math.random() * 100);

    posX += dx;
    posY += dy;

    // Wrap-around: om knappen lämnar skärmen, kommer den in från motsatt sida
    if(posX < -nejButton.offsetWidth) posX = window.innerWidth;
    if(posX > window.innerWidth) posX = -nejButton.offsetWidth;
    if(posY < -nejButton.offsetHeight) posY = window.innerHeight;
    if(posY > window.innerHeight) posY = -nejButton.offsetHeight;

    // Skala ner knappen lite när den flyttar sig
    const scale = Math.max(0.5, 1 - (150 - distance)/300);
    nejButton.style.transform = `scale(${scale})`;

    nejButton.style.left = posX + 'px';
    nejButton.style.top = posY + 'px';
  } else {
    // Normal storlek när musen är långt borta
    nejButton.style.transform = 'scale(1)';
  }
});
</script>

</body>
</html>
