<html>
<head>
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
  height: 550px;     
  background: white;

  border-radius: 40px;
  position: relative; /* gör det möjligt att positionera bilden inuti */
}

.center-box img {
  position: absolute;
  top: 20px;           /* lite avstånd från toppen */
  left: 50%;           /* horisontellt centrerad */
  transform: translateX(-50%); /* centrerar exakt */
  width: 50px;         /* exakt bredd */
  height: 50px;        /* exakt höjd */
  border-radius: 10px; /* valfritt: rundade hörn på bilden */
}
</style>
</head>

<body>

<div class="center-box">
  <img src="https://thumbs.dreamstime.com/b/print-206284399.jpg" alt="Bild">
</div>

</body>
</html>
