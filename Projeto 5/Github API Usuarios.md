## Projeto 5: Github API Usuário

**Descrição:**
O GitHub User Explorer é uma aplicação web simples e elegante que permite aos usuários explorarem informações de outros usuários do GitHub. Basta inserir o nome de usuário desejado, e a aplicação buscará e exibirá informações relevantes sobre o perfil do usuário no GitHub.

**Funcionalidades:**

1. **Buscar Usuário:** Insira o nome de usuário do GitHub na caixa de pesquisa.
2. **Exibir Informações:** As informações do usuário, como nome, seguidores, repositórios públicos, biografia e avatar, serão exibidas de forma clara e organizada.
3. **Estilo Moderno:** O projeto possui um design moderno e atraente, com bordas arredondadas, sombras suaves e cores agradáveis.
4. **Validação de Entrada:** Garante que o campo de entrada não está vazio antes de realizar a busca, exibindo mensagens de erro apropriadas.
5. **Interatividade:** Botão de busca interativo com efeito visual ao passar o mouse.
6. **Tratamento de Erros:** Mensagens de erro amigáveis são exibidas se ocorrer algum problema durante a busca.

```python
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>GitHub User Info</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>

    <div class="container">
        <label for="username">Digite o nome de usuário do GitHub:</label>
        <input type="text" id="username" placeholder="Digite o nome de usuário">
        <button onclick="getUserInfo()">Buscar</button>

        <div id="result-container">
            <!-- Aqui serão exibidas as informações do usuário -->
        </div>
    </div>

    <script src="https://code.jquery.com/jquery-3.6.4.min.js"></script>
    <script src="script.js"></script>
</body>
</html>
```

```python
body {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  background-color: #f5f5f5;
  display: flex; 
  justify-content: center; 
  margin: 0;
}

.container {
  text-align: center;
  background-color: #fff;
  padding: 30px;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  width: 400px;
}

#username {
  width: 100%;
  padding: 10px;
  box-sizing: border-box;
  margin-bottom: 20px;
  border: 1px solid #ddd;
  border-radius: 4px;
}

button {
  background-color: #4caf50;
  color: white;
  padding: 10px 20px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s;
}

button:hover {
  background-color: #45a049;
}

#result-container {
  margin-top: 20px;
  text-align: left;
}

h2 {
  color: #333;
}

p {
  color: #555;
}

.error {
  color: #d9534f;
  margin-top: 10px;
}
```

```python
function getUserInfo() {
  const username = $('#username').val();

  if (username.trim() !== '') {
      $.ajax({
          url: `https://api.github.com/users/${username}`,
          method: 'GET',
          success: function (data) {
              displayUserInfo(data);
          },
          error: function (error) {
              displayError(error.responseJSON.message);
          }
      });
  } else {
      displayError('Por favor, insira um nome de usuário válido.');
  }
}

function displayUserInfo(user) {
  const resultContainer = $('#result-container');
  resultContainer.html(`
      <h2>${user.name}</h2>
      <p>Seguidores: ${user.followers}</p>
      <p>Repositórios públicos: ${user.public_repos}</p>
      <p>Biografia: ${user.bio}</p>
      <img src="${user.avatar_url}" alt="Avatar" width="100">
  `);
}

function displayError(message) {
  const resultContainer = $('#result-container');
  resultContainer.html(`<p class="error">${message}</p>`);
}
```