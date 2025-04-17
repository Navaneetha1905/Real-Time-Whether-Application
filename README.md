<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Weather App</title>
  <link rel="stylesheet" href="style.css">
  

  <style>
    body {
      font-family: Arial, sans-serif;
      text-align: center;
      background-color: #f0f8ff;
      margin: 0;
      padding: 0;
    }
    .weather-container {
      max-width: 500px;
      margin: 50px auto;
      padding: 20px;
      background: #ffffff;
      border-radius: 10px;
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
    }
    input {
      padding: 10px;
      font-size: 16px;
      width: 80%;
      margin-bottom: 10px;
      border: 1px solid #ccc;
      border-radius: 5px;
    }
    button {
      padding: 10px 20px;
      font-size: 16px;
      background-color: #007bff;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }
    button:hover {
      background-color: #0056b3;
    }
    .weather-info {
      margin-top: 20px;
    }
  </style>
</head>
<body>
  <div class="weather-container">
    
    <h1>🌤️Weather App</h1>
    <input type="text" id="city" placeholder="Enter city name" />
    <button onclick="getWeather()">Get Weather</button>
    <div class="weather-info" id="weather-info">
      <!-- Weather information will appear here -->
    </div>
  </div>

  <script>
    async function getWeather() {
      const city = document.getElementById('city').value.trim();
      const apiKey = '7cbc3f57935f827159829c6c4f66bb64'; // Replace with your OpenWeatherMap API key

      if (!city) {
        document.getElementById('weather-info').innerHTML = "<p>Please enter a city name.</p>";
        return;
      }

      const apiUrl = `https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=${apiKey}&units=metric`;

      try {
        const response = await fetch(apiUrl);
        if (!response.ok) {
          throw new Error('City not found');
        }
        const data = await response.json();
        const weatherInfo = `
          <h2>${data.name}, ${data.sys.country}</h2>
          <p>Temperature: ${data.main.temp}°C</p>
          <p>Weather: ${data.weather[0].description}</p>
          <p>Humidity: ${data.main.humidity}%</p>
        `;
        document.getElementById('weather-info').innerHTML = weatherInfo;
      } catch (error) {
        document.getElementById('weather-info').innerHTML = `<p>${error.message}</p>`;
      }
    }
  </script>
</body>
</html>

