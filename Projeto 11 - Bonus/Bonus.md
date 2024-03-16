**Projeto 11 - Bonus**

Rodem no pc de vcs e Divirtam-se.

index.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mapa Interativo com Leaflet</title>
    <link rel="stylesheet" href="https://unpkg.com/leaflet/dist/leaflet.css" />
</head>
<body>

    <!-- Adicione este campo no seu HTML -->
    <input type="text" id="cep-input" placeholder="Digite o CEP">
    <button id="search-button">Buscar</button>

    <!-- Adicione este campo no seu HTML -->
    <input type="text" id="address-input" placeholder="Digite o endereço">
    <button id="search-address-button">Buscar por Endereço</button>

    <div id="map" style="height: 400px;"></div>
    
    <script src="https://code.jquery.com/jquery-3.6.4.min.js"></script>
    <script src="https://unpkg.com/leaflet/dist/leaflet.js"></script>
    <script src="script.js"></script>
</body>
</html>
```

script.js 

```jsx
// script.js

// Inicializa o mapa
var mymap = L.map('map').setView([-23.550520, -46.633308], 13);
var marker; // Variável para armazenar o marcador no mapa

// Adiciona o provedor de mapas do OpenStreetMap
L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
    attribution: '© OpenStreetMap contributors'
}).addTo(mymap);

// Adiciona um marcador padrão em São Paulo
marker = L.marker([-23.550520, -46.633308]).addTo(mymap);

// Adiciona uma popup ao marcador
marker.bindPopup("<b>São Paulo, Brasil</b><br>Um ponto interessante.").openPopup();

// Adiciona um evento de clique no botão de busca por CEP
$('#search-button').on('click', function () {
    // Obtém o CEP do campo de entrada
    var cep = $('#cep-input').val();
    
    // Verifica se o CEP está no formato válido
    if (/^\d{5}-\d{3}$/.test(cep)) {
        // Chama a função para obter as coordenadas a partir do CEP
        getCoordinatesFromCEP(cep);
    } else {
        alert('Formato de CEP inválido. Por favor, digite no formato 12345-678.');
    }
});

// Função para obter coordenadas a partir do CEP usando a API do OpenStreetMap
function getCoordinatesFromCEP(cep) {
    $.ajax({
        url: `https://nominatim.openstreetmap.org/search?format=json&postalcode=${cep}&country=Brazil`,
        method: 'GET',
        dataType: 'json',
        success: function (data) {
            // Verifica se há resultados válidos
            if (data && data.length > 0) {
                // Obtém as coordenadas do primeiro resultado
                var lat = parseFloat(data[0].lat);
                var lon = parseFloat(data[0].lon);

                // Atualiza a posição do marcador no mapa
                updateMarkerPosition(lat, lon);

                // Ajusta a visualização do mapa para a nova localização
                mymap.setView([lat, lon], 13);
            } else {
                alert('CEP não encontrado. Por favor, verifique o CEP digitado.');
            }
        },
        error: function (error) {
            console.error('Erro ao obter coordenadas do CEP:', error);
            alert('Ocorreu um erro ao obter as coordenadas do CEP. Por favor, tente novamente.');
        }
    });
}

// Adiciona um evento de clique no botão de busca por endereço
$('#search-address-button').on('click', function () {
    // Obtém o endereço do campo de entrada
    var address = $('#address-input').val();

    // Chama a função para obter as coordenadas a partir do endereço
    getCoordinatesFromAddress(address);
});

// Função para obter coordenadas a partir do endereço usando a API do OpenStreetMap
function getCoordinatesFromAddress(address) {
    $.ajax({
        url: `https://nominatim.openstreetmap.org/search?format=json&q=${encodeURIComponent(address)}`,
        method: 'GET',
        dataType: 'json',
        success: function (data) {
            // Verifica se há resultados válidos
            if (data && data.length > 0) {
                // Obtém as coordenadas do primeiro resultado
                var lat = parseFloat(data[0].lat);
                var lon = parseFloat(data[0].lon);

                // Atualiza a posição do marcador no mapa
                updateMarkerPosition(lat, lon);

                // Ajusta a visualização do mapa para a nova localização
                mymap.setView([lat, lon], 13);
            } else {
                alert('Endereço não encontrado. Por favor, verifique o endereço digitado.');
            }
        },
        error: function (error) {
            console.error('Erro ao obter coordenadas do endereço:', error);
            alert('Ocorreu um erro ao obter as coordenadas do endereço. Por favor, tente novamente.');
        }
    });
}

// Função para atualizar a posição do marcador no mapa
function updateMarkerPosition(lat, lon) {
    // Remove o marcador existente (se houver)
    if (marker) {
        mymap.removeLayer(marker);
    }

    // Adiciona um novo marcador na nova posição
    marker = L.marker([lat, lon]).addTo(mymap);

    // Adiciona uma popup ao marcador
    marker.bindPopup(`<b>Localização do CEP</b><br>Latitude: ${lat}<br>Longitude: ${lon}`).openPopup();
}
```

Rotas 

```python
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mapa Interativo com Leaflet</title>
    <link rel="stylesheet" href="https://unpkg.com/leaflet/dist/leaflet.css" />

    <!-- Inclua este link no cabeçalho do seu HTML antes do script.js -->
    <link rel="stylesheet" href="https://unpkg.com/leaflet-routing-machine/dist/leaflet-routing-machine.css" />

</head>
<body>

    <!-- Adicione estes campos no seu HTML -->
    <label for="address-input-A">Endereço Ponto A:</label>
    <input type="text" id="address-input-A" placeholder="Digite o endereço do Ponto A">

    <label for="address-input-B">Endereço Ponto B:</label>
    <input type="text" id="address-input-B" placeholder="Digite o endereço do Ponto B">

    <button id="search-route-button">Buscar Rota</button>

    <div id="map" style="height: 400px;"></div>
    
    <script src="https://code.jquery.com/jquery-3.6.4.min.js"></script>
    
    <script src="https://unpkg.com/leaflet/dist/leaflet.js"></script>
    <script src="https://unpkg.com/leaflet-routing-machine/dist/leaflet-routing-machine.js"></script>
 
    <script src="script.js"></script>
</body>
</html>
```

```python
// script.js

// Cria um mapa Leaflet e define a visualização inicial
var mymap = L.map('map').setView([-23.550520, -46.633308], 13);

// Declaração de variáveis para os marcadores A e B, e o controle de rota
var markerA, markerB;
var routingControl;

// Adiciona um layer do OpenStreetMap ao mapa
L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
    attribution: '© OpenStreetMap contributors'
}).addTo(mymap);

// Adiciona marcadores iniciais A e B ao mapa com popups
// markerA = L.marker([-23.550520, -46.633308]).addTo(mymap);
// markerA.bindPopup("<b>Ponto A</b><br>São Paulo, Brasil.").openPopup();

// markerB = L.marker([-23.559616, -46.658920]).addTo(mymap);
// markerB.bindPopup("<b>Ponto B</b><br>Outro local em São Paulo.").openPopup();

// Função para criar a rota entre os pontos A e B
function createRoute() {
    // Remove a rota existente (se houver)
    if (routingControl) {
        mymap.removeControl(routingControl);
    }

    // Cria um novo controle de rota
    routingControl = L.Routing.control({
        waypoints: [
            L.latLng(markerA.getLatLng()), // Ponto A
            L.latLng(markerB.getLatLng())  // Ponto B
        ],
        routeWhileDragging: true
    }).addTo(mymap);
}

// Adiciona um evento de clique no botão de busca por rota
$('#search-route-button').on('click', function () {
    // Obtém o endereço do ponto A do campo de entrada
    var addressA = $('#address-input-A').val();
    // Obtém o endereço do ponto B do campo de entrada
    var addressB = $('#address-input-B').val();

    // Chama a função para obter as coordenadas a partir dos endereços
    getCoordinatesFromAddress(addressA, 'A');
    getCoordinatesFromAddress(addressB, 'B');
});

// Adiciona um evento de clique no botão de limpar rota
$('#clear-route-button').on('click', function () {
    // Remove a rota existente (se houver)
    if (routingControl) {
        mymap.removeControl(routingControl);
    }
});

// Função para obter coordenadas a partir do endereço usando a API do OpenStreetMap
function getCoordinatesFromAddress(address, point) {
    $.ajax({
        url: `https://nominatim.openstreetmap.org/search?format=json&q=${encodeURIComponent(address)}`,
        method: 'GET',
        dataType: 'json',
        success: function (data) {
            // Verifica se há resultados válidos
            if (data && data.length > 0) {
                // Obtém as coordenadas do primeiro resultado
                var lat = parseFloat(data[0].lat);
                var lon = parseFloat(data[0].lon);

                // Atualiza a posição do marcador no mapa
                updateMarkerPosition(lat, lon, point);

                // Ajusta a visualização do mapa para a nova localização
                mymap.setView([lat, lon], 13);

                // Cria a rota entre os pontos A e B
                createRoute();
            } else {
                alert(`Endereço do ponto ${point} não encontrado. Por favor, verifique o endereço digitado.`);
            }
        },
        error: function (error) {
            console.error(`Erro ao obter coordenadas do ponto ${point}:`, error);
            alert(`Ocorreu um erro ao obter as coordenadas do ponto ${point}. Por favor, tente novamente.`);
        }
    });
}

// Função para atualizar a posição do marcador no mapa
function updateMarkerPosition(lat, lon, point) {
    // Remove o marcador existente (se houver)
    if (point === 'A') {
        if (markerA) {
            mymap.removeLayer(markerA);
        }
        // Adiciona um novo marcador na nova posição para o ponto A
        markerA = L.marker([lat, lon]).addTo(mymap);
        markerA.bindPopup(`<b>Ponto A</b><br>Latitude: ${lat}<br>Longitude: ${lon}`).openPopup();
    } else if (point === 'B') {
        if (markerB) {
            mymap.removeLayer(markerB);
        }
        // Adiciona um novo marcador na nova posição para o ponto B
        markerB = L.marker([lat, lon]).addTo(mymap);
        markerB.bindPopup(`<b>Ponto B</b><br>Latitude: ${lat}<br>Longitude: ${lon}`).openPopup();
    }
}
```