## Projeto 6: Galeria de Imagem

Crie uma galeria de imagens onde os usuários podem navegar por diferentes imagens com transições suaves. Use jQuery para manipulação do DOM e animações.

index.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Galeria de Imagens</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>

    <div class="gallery-container">
        <div class="gallery">
            <img src="img/image1.jpg" alt="Imagem 1">
            <img src="img/image2.jpg" alt="Imagem 2">
            <img src="img/image3.jpg" alt="Imagem 3">
            <!-- Adicione mais imagens conforme necessário -->

            <div class="nav-btn prev">&#10094;</div>
            <div class="nav-btn next">&#10095;</div>
        </div>
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
  justify-content: center; 
  margin: 0;
}

.gallery-container {
  position: relative;
}

.gallery {
  display: flex;
  overflow: hidden;
  max-width: 600px;
  margin: 0 auto;
}

.gallery img {
  width: 100%;
  transition: transform 0.5s ease;
}

.nav-btn {
  position: absolute;
  top: 50%;
  font-size: 24px;
  cursor: pointer;
  user-select: none;
}

.prev {
  left: 10px;
}

.next {
  right: 10px;
}
```

script.js

```jsx
$(document).ready(function () {
  let currentIndex = 0;
  const totalImages = $('.gallery img').length;

  $('.next').on('click', function () {
      showImage(currentIndex + 1);
  });

  $('.prev').on('click', function () {
      showImage(currentIndex - 1);
  });

  function showImage(index) {
      if (index >= 0 && index < totalImages) {
          currentIndex = index;
          const translateValue = -index * 100 + '%';
          $('.gallery img').css('transform', 'translateX(' + translateValue + ')');
      }
  }
});
```