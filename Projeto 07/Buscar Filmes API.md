**Projeto 7: Buscar Filmes API**

Aplicativo de busca de filmes que consome a API pública do OMDB (The Open Movie Database)

[https://www.omdbapi.com](https://www.omdbapi.com/)

index.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Busca de Filmes</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>

    <div class="search-container">
        <label for="movie-search">Digite o nome do filme:</label>
        <input type="text" id="movie-search" placeholder="Digite o nome do filme">
        <button onclick="searchMovie()">Buscar</button>

        <div id="movie-details"></div>
    </div>

    <script src="https://code.jquery.com/jquery-3.6.4.min.js"></script>
    <script src="script.js"></script>

</body>
</html>
```

styles.css

```css
body {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  background-color: #f5f5f5;
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100vh;
  margin: 0;
}

.search-container {
  text-align: center;
  background-color: #fff;
  padding: 30px;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  max-width: 400px;
}

#movie-details {
  margin-top: 20px;
  text-align: left;
}
```

scripts.js

```jsx
function searchMovie() {
    const apiKey = ''; // Substitua pelo seu próprio API Key do OMDB
    const movieTitle = $('#movie-search').val();

    if (movieTitle.trim() !== '') {
        $.ajax({
            url: `https://www.omdbapi.com/?apikey=${apiKey}&t=${movieTitle}`,
            method: 'GET',
            success: function (data) {
                displayMovieDetails(data);
            },
            error: function (error) {
                displayError('Filme não encontrado. Verifique o título e tente novamente.');
            }
        });
    } else {
        displayError('Por favor, insira o nome do filme.');
    }
}

function displayMovieDetails(movie) {
    const movieDetailsContainer = $('#movie-details');
    movieDetailsContainer.empty();

    if (movie.Response === 'True') {
        movieDetailsContainer.append(`
            <h2>${movie.Title}</h2>
            <p><strong>Ano:</strong> ${movie.Year}</p>
            <p><strong>Classificação:</strong> ${movie.Rated}</p>
            <p><strong>Elenco:</strong> ${movie.Actors}</p>
            <p><strong>Enredo:</strong> ${movie.Plot}</p>
            <img src="${movie.Poster}" alt="${movie.Title}" width="200">
        `);
    } else {
        displayError('Filme não encontrado. Verifique o título e tente novamente.');
    }
}

function displayError(message) {
    const movieDetailsContainer = $('#movie-details');
    movieDetailsContainer.empty();
    movieDetailsContainer.append(`<p class="error">${message}</p>`);
}
```