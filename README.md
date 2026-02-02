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
  transition: transform 0.2s, left 0.3s, top 0.3s;
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
  background-color: #b0b0b0; /* mörkare grå */
  color: #333;
  position: relative;
}

/* Container för knappar bredvid varandra */
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

// Lyssna på musrörelser
document.addEventListener('mousemove', e => {
  const rect = nejButton.getBoundingClientRect();
  const mouseX = e.clientX;
  const mouseY = e.clientY;
  
  const buttonCenterX = rect.left + rect.width / 2;
  const buttonCenterY = rect.top + rect.height / 2;
  
  const distance = Math.hypot(mouseX - buttonCenterX, mouseY - buttonCenterY);

  // Om musen är nära (t.ex. <100px), flytta knappen
  if(distance < 100) {
    const offsetX = (buttonCenterX - mouseX) / distance * 120; // flytta bort
    const offsetY = (buttonCenterY - mouseY) / distance * 60; // lite vertikalt
    nejButton.style.transform = `translate(${offsetX}px, ${offsetY}px)`;
  } else {
    nejButton.style.transform = 'translate(0,0)';
  }
});
</script>

</body>
</html>

