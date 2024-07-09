# Projeto 2: Formulário de contato utilizando HTML, CSS e jQuery

Neste exemplo, usaremos jQuery para validar e processar o formulário de contato. Aqui está o código comentado:

```python
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Formulário de Contato</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>

    <div class="container">
        <h1>Entre em Contato</h1>
        <form id="contactForm">
            <label for="name">Nome:</label>
            <input type="text" id="name" name="name">

            <label for="email">E-mail:</label>
            <input type="email" id="email" name="email">

            <label for="message">Mensagem:</label>
            <textarea id="message" name="message" rows="4"></textarea>

            <button type="submit">Enviar</button>
        </form>
    </div>

    <script src="https://code.jquery.com/jquery-3.6.4.min.js"></script>
    <script src="script.js"></script>
</body>
</html>
```

```python
$(document).ready(function() {
  // Intercepta o envio do formulário
  $('#contactForm').submit(function(event) {
      // Impede o envio padrão do formulário
      event.preventDefault();

      // Validação simples (pode ser expandida conforme necessário)
      var name = $('#name').val();
      var email = $('#email').val();
      var message = $('#message').val();

      if (name === '' || email === '' || message === '') {
          alert('Por favor, preencha todos os campos do formulário.');
          return;
      }

      // Simulação de envio bem-sucedido (pode ser substituído por uma solicitação AJAX real)
      alert('Formulário enviado com sucesso!\nNome: ' + name + '\nE-mail: ' + email + '\nMensagem: ' + message);

      // Limpa os campos do formulário após o envio
      $('#name, #email, #message').val('');
  });
});
```

```python
body {
  font-family: Arial, sans-serif;
  background-color: #f4f4f4;
  margin: 0;
  padding: 0;
  display: flex; 
  justify-content: center; 
}

.container {
  background-color: #fff;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

h1 {
  text-align: center;
  color: #333;
}

form {
  display: flex;
  flex-direction: column;
}

label {
  margin-bottom: 8px;
}

input, textarea {
  padding: 8px;
  margin-bottom: 16px;
}

button {
  padding: 10px;
  cursor: pointer;
}
```