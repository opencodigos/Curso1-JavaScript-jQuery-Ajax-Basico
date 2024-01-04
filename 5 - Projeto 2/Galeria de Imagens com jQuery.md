# Projeto 2: Galeria de Imagens com jQuery

Crie uma galeria de imagens simples usando HTML, CSS e jQuery. Este projeto ajudará a entender como selecionar elementos, manipular o DOM usando jQuery e adicionar efeitos visuais.

**Funcionalidades:**

1. Exibir uma grade de miniaturas de imagens.
2. Ao clicar em uma miniatura, exibir a imagem em tamanho real com efeitos de transição.
3. Adicionar um botão de "próxima" e "anterior" para navegar pelas imagens.

**index.html**

```python
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link rel="stylesheet" href="styles.css">
  <title>Galeria de Imagens</title>
</head>
<body>
  <div class="gallery-container">
    <div class="thumbnails">
      <img src="img/image1-thumb.jpg" alt="Thumbnail 1" data-image="img/image1.jpg">
      <img src="img/image2-thumb.jpg" alt="Thumbnail 2" data-image="img/image2.jpg">
      <img src="img/image3-thumb.jpg" alt="Thumbnail 3" data-image="img/image3.jpg">
      <!-- Adicione mais miniaturas conforme necessário -->
    </div>
    <div class="main-image">
      <img id="mainImage" src="" alt="Main Image">
      <div class="nav-buttons">
        <button id="prevBtn">Anterior</button>
        <button id="nextBtn">Próxima</button>
      </div>
    </div>
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

.gallery-container {
  text-align: center;
}

.thumbnails img {
  width: 100px;
  height: 100px;
  margin: 5px;
  cursor: pointer;
}

.main-image {
  margin-top: 20px;
}

#mainImage {
  max-width: 100%;
  max-height: 400px;
  transition: opacity 0.5s ease-in-out;
}

.nav-buttons {
  margin-top: 10px;
}

button {
  padding: 8px;
  cursor: pointer;
}
```

**script.js**

```python
$(document).ready(function () {
  var currentIndex = 0;
  var $thumbnails = $('.thumbnails img');
  var $mainImage = $('#mainImage');

  // Exibir a imagem principal ao clicar na miniatura
  $thumbnails.on('click', function () {
    currentIndex = $thumbnails.index(this);
    showImage(currentIndex);
  });

  // Exibir a próxima imagem ao clicar no botão "Próxima"
  $('#nextBtn').on('click', function () {
    currentIndex = (currentIndex + 1) % $thumbnails.length;
    showImage(currentIndex);
  });

  // Exibir a imagem anterior ao clicar no botão "Anterior"
  $('#prevBtn').on('click', function () {
    currentIndex = (currentIndex - 1 + $thumbnails.length) % $thumbnails.length;
    showImage(currentIndex);
  });

  // Função para exibir a imagem na posição index
  function showImage(index) {
    var imageUrl = $thumbnails.eq(index).data('image');
    $mainImage.fadeOut(300, function () {
      $mainImage.attr('src', imageUrl).fadeIn(300);
    });
  }
});
```