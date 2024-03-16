**Projeto 8: Busca Dinâmica com jQuery**

index.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Lista de Postagens</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body> 
    <div class="search-container">
        <button id="clear-button">Limpar</button>
        <label for="search-input">Digite para buscar postagens:</label>
        <input type="text" id="search-input" placeholder="Digite aqui">
        <div id="suggestions-container"></div>
    </div>

    <div id="post-list"></div>  
    <script src="https://code.jquery.com/jquery-3.6.4.min.js"></script>
    <script src="script.js"></script>
</body>
</html>
```

styles.css

```
body {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  background-color: #f5f5f5;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center; 
  margin: 0;
}

.search-container {
  position: absolute;
  top: 0;
  text-align: center;
  background-color: #fff;
  padding: 30px;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  max-width: 400px;
  margin-bottom: 20px;
}

#suggestions-container { 
  margin-top: 10px;
}

.suggestion {
  cursor: pointer;
  padding: 8px;
  border-bottom: 1px solid #ddd;
}

.suggestion:hover {
  background-color: #f9f9f9;
}

#post-list {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  margin-top: 150px;
}

.post {
  width: 200px;
  margin: 10px;
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 8px;
  max-width: 200px;
  text-align: center;
}

.post img {
  max-width: 100%;
  border-radius: 4px; 
}
```

scripts.js

```jsx
$(document).ready(function () {
    const searchInput = $('#search-input');
    const suggestionsContainer = $('#suggestions-container');
    const postList = $('#post-list');
    const clearButton = $('#clear-button'); // Adiciona a referência ao botão de limpar

    let allPosts;

    // Realiza uma chamada AJAX para obter os dados do arquivo JSON
    $.ajax({
        url: 'posts.json',
        method: 'GET',
        dataType: 'json',
        success: function (data) {
            allPosts = data;
            // Atualiza a lista de postagens inicialmente
            updatePostList(allPosts);
        },
        error: function (error) {
            console.error('Erro ao carregar postagens:', error);
        }
    });

    searchInput.on('input', function () {
        const query = searchInput.val().toLowerCase();

        if (query.trim() !== '') {
            const filteredPosts = allPosts.filter(post => post.title.toLowerCase().includes(query));
            displaySuggestions(filteredPosts);
        } else {
            suggestionsContainer.empty();
        }
    });

    clearButton.on('click', function () {
        // Limpa o campo de busca e reexibe todas as postagens
        searchInput.val('');
        updatePostList(allPosts);
    });

    function displaySuggestions(suggestedPosts) {
        suggestionsContainer.empty();

        suggestedPosts.forEach(function (post) {
            const suggestionItem = $('<div class="suggestion"></div>');
            suggestionItem.text(post.title);
            suggestionItem.on('click', function () {
                searchPostByTitle(post.title);
                suggestionsContainer.empty();
            });

            suggestionsContainer.append(suggestionItem);
        });
    }

    function updatePostList(posts) {
        postList.empty();

        posts.forEach(function (post) {
            const postItem = $('<div class="post"></div>');
            postItem.append(`<h3>${post.title}</h3>`);
            postItem.append(`<img src="${post.image}" alt="${post.title}">`);
            postList.append(postItem);
        });
    }

    function searchPostByTitle(title) {
        const foundPost = allPosts.find(post => post.title === title);

        if (foundPost) {
            updatePostList([foundPost]);
        }
    }
});
```

posts.json

```json
[
    { "title": "Web com Python e Django", "image": "https://via.placeholder.com/150" },
    { "title": "Como aprender Javascript", "image": "https://via.placeholder.com/150" },
    { "title": "Projetos Incríveis com AJAX", "image": "https://via.placeholder.com/150" },
    { "title": "Introdução ao HTML5", "image": "https://via.placeholder.com/150" },
    { "title": "CSS Responsivo", "image": "https://via.placeholder.com/150" },
    { "title": "Node.js: Uma visão geral", "image": "https://via.placeholder.com/150" },
    { "title": "Desenvolvimento Web Moderno", "image": "https://via.placeholder.com/150" },
    { "title": "React.js: Uma introdução", "image": "https://via.placeholder.com/150" },
    { "title": "Bootstrap vs. Materialize", "image": "https://via.placeholder.com/150" },
    { "title": "Python para Iniciantes", "image": "https://via.placeholder.com/150" },
    { "title": "APIs RESTful: O que você precisa saber", "image": "https://via.placeholder.com/150" },
    { "title": "UI/UX Design: Princípios Básicos", "image": "https://via.placeholder.com/150" },
    { "title": "Inteligência Artificial na Indústria", "image": "https://via.placeholder.com/150" },
    { "title": "Sass vs. Less: Uma comparação", "image": "https://via.placeholder.com/150" },
    { "title": "WebAssembly: O futuro da web", "image": "https://via.placeholder.com/150" },
    { "title": "Firebase: Uma visão geral", "image": "https://via.placeholder.com/150" },
    { "title": "Machine Learning para todos", "image": "https://via.placeholder.com/150" },
    { "title": "JAMstack: O que é e por que você deve usá-lo", "image": "https://via.placeholder.com/150" },
    { "title": "Segurança na Web: Melhores práticas", "image": "https://via.placeholder.com/150" },
    { "title": "GraphQL: Uma visão prática", "image": "https://via.placeholder.com/150" }
]
```