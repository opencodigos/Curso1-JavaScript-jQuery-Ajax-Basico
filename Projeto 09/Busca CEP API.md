**Projeto 9: Busca CEP API**

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Consulta de CEP</title> 
    <link rel="stylesheet" href="styles.css">
</head>
<body>

    <div class="container">
        <label for="cepInput">Digite o CEP: </label>
        <input type="text" id="cepInput" maxlength="9" placeholder="Ex: 00000-000">
        <button onclick="consultarCEP()">Consultar</button> 
        <div id="result" class="invisible"></div>
    </div> 
    <script src="https://code.jquery.com/jquery-3.6.4.min.js"></script>
    <script src="script.js"></script> 
</body>
</html>
```

```css
body {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  display: flex;
  justify-content: center; 
  margin: 0;
  background-color: #f5f5f5;
}

.container {
  background-color: #fff;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  padding: 20px;
  text-align: center;
  transition: box-shadow 0.3s ease;
  width: 300px;
}

label {
  display: block;
  margin-bottom: 10px;
}

input {
  width: calc(100% - 22px);
  padding: 10px;
  margin-bottom: 15px;
  border: 1px solid #ccc;
  border-radius: 5px;
  transition: border-color 0.3s ease;
}

input:focus {
  outline: none;
  border-color: #4caf50;
}

button {
  background-color: #4caf50;
  color: #fff;
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

button:hover {
  background-color: #45a049;
}

#result {
  text-align: left;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
  margin-top: 20px;
  max-width: 300px;
  margin-left: auto;
  margin-right: auto;
  opacity: 0;
  transition: opacity 0.3s ease;
}

#result p {
  margin: 0 0 10px;
}

#result.visible {
  opacity: 1;
}
```

```jsx
function consultarCEP() {
    const cepInput = $('#cepInput');
    const resultDiv = $('#result');
    const cep = cepInput.val().replace(/\D/g, '');

    resultDiv.removeClass('visible');

    if (cep.length !== 8) {
        alert('Digite um CEP válido');
        return;
    }

    $.get(`https://viacep.com.br/ws/${cep}/json/`, function(data) {
        exibirResultado(data);
    });
}

function exibirResultado(resultado) {
    const resultDiv = $('#result');
    resultDiv.html(`
        <p><strong>Logradouro:</strong> ${resultado.logradouro}</p>
        <p><strong>Bairro:</strong> ${resultado.bairro}</p>
        <p><strong>Cidade:</strong> ${resultado.localidade}</p>
        <p><strong>UF:</strong> ${resultado.uf}</p>
    `);
    resultDiv.addClass('visible');
}
```