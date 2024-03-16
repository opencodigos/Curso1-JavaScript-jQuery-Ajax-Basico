# Projeto 3: Aplicativo de Previsão do Tempo com AJAX

Desenvolva um aplicativo de previsão do tempo usando HTML, CSS, JavaScript e AJAX para obter dados assíncronos da API de previsão do tempo. Este projeto abordará conceitos de requisições assíncronas, manipulação de JSON e uso de promessas.

**Funcionalidades:**

- Permitir que o usuário insira a cidade desejada.
- Ao clicar em um botão, realizar uma requisição AJAX para obter dados de previsão do tempo.
- Exibir informações relevantes (temperatura, condições meteorológicas, etc.) na página.
- Lidar com erros e fornecer uma experiência de usuário amigável.

https://openweathermap.org/

**index.html**

```python
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link rel="stylesheet" href="styles.css">
  <title>Previsão do Tempo</title>
</head>
<body>
  <div class="container">
    <h1>Previsão do Tempo</h1>
    <input type="text" id="cityInput" placeholder="Digite a cidade">
    <button id="getWeatherBtn">Obter Previsão</button>
    <div id="weatherInfo"></div>
  </div>
  <script src="https://code.jquery.com/jquery-3.6.4.min.js"></script>
  <script src="script.js"></script>
</body>
</html>
```

**styles.css**

```python
body {
  font-family: Arial, sans-serif;
  margin: 0;
  padding: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background-color: #f4f4f4;
}

.container {
  text-align: center;
}

input {
  padding: 8px;
  margin-right: 5px;
}

button {
  padding: 8px;
  cursor: pointer;
}

#weatherInfo {
  margin-top: 20px;
}
```

**script.js**

```python
$(document).ready(function () {
  $('#getWeatherBtn').on('click', function () {
    var city = $('#cityInput').val();
    if (city.trim() !== '') {
      getWeather(city);
    }
  });

  function getWeather(city) {
    var apiKey = '6880cfc5f3db94c5cd88de15eeb8a314';
    var apiUrl = 'https://api.openweathermap.org/data/2.5/weather';

    $.ajax({
      url: apiUrl,
      type: 'GET',
      data: {
        q: city,
        appid: apiKey,
        units: 'metric', // Use 'imperial' for Fahrenheit
      },
      success: function (data) {
        displayWeather(data);
      },
      error: function (error) {
        showError();
      }
    });
  }

  function displayWeather(data) {
    var weatherInfo = `
      <h2>${data.name}, ${data.sys.country}</h2>
      <p>Temperatura: ${data.main.temp} °C</p>
      <p>Condição: ${data.weather[0].description}</p>
      <p>Umidade: ${data.main.humidity} %</p>
    `;
    $('#weatherInfo').html(weatherInfo);
  }

  function showError() {
    $('#weatherInfo').html('<p>Erro ao obter a previsão do tempo. Por favor, tente novamente.</p>');
  }
});
```