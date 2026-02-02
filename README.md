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
  padding-top: 20px; /* avstånd från toppen */
}

.center-box img {
  width: 200px;         
  height: 200px;        
  border-radius: 10px; 
  margin-bottom: 20px; /* avstånd mellan bild och textruta */
}

.text-box {
  width: 700px;
  background-color: #FFFFFF; /* ljusare rosa */
  border-radius: 20px;
  padding: 10px;

  /* Bold Noto Sans Japanese */
  font-family: 'Noto Sans JP', sans-serif;
  font-weight: 700;
  font-size: 40px;
  color: #333;

  text-align: center;
  word-wrap: break-word; /* bryter texten om den blir för lång */
}

/* Ny knappstil */
.button {
  width: 200px;      /* mindre bredd */
  height: 70px;      /* mindre höjd */
  background-color: #ff69b4; /* stark rosa */
  color: white;
  font-family: 'Noto Sans JP', sans-serif;
  font-weight: 700;
  font-size: 20px;
  border: none;
  border-radius: 50px; /* rundare hörn */
  cursor: pointer;
  margin-top: 20px;
  align-self: flex-end; /* placerar knappen mer åt höger */
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  transition: transform 0.2s; /* enkel hover-effekt */
}

.button:hover {
  transform: scale(1.05); /* liten förstoring vid hover */
}
</style>
</head>

<body>

<div class="center-box">
  <img src="https://thumbs.dreamstime.com/b/print-206284399.jpg" alt="Bild">
  <div class="text-box">
    ... vill du bli min valentine?
  </div>
  <button class="button">Klicka här</button>
</div>

</body>
</html>
