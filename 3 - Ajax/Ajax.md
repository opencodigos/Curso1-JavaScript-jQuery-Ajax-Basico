# Ajax 

O AJAX (Asynchronous JavaScript and XML) é uma técnica que permite realizar requisições assíncronas no navegador, atualizando partes específicas de uma página sem a necessidade de recarregar a página inteira.

### **Exemplo básico com XMLHttpRequest:**

```python
<!-- HTML -->
<button id="loadData">Carregar Dados</button>
<div id="output"></div>

<!-- JavaScript -->
<script>
  document.getElementById("loadData").addEventListener("click", function() {
    var xhr = new XMLHttpRequest();

    xhr.onreadystatechange = function() {
      if (xhr.readyState === 4 && xhr.status === 200) {
        var data = JSON.parse(xhr.responseText);
        document.getElementById("output").innerHTML = data.message;
      }
    };

    xhr.open("GET", "https://api.example.com/data", true);
    xhr.send();
  });
</script>
```

### **Trabalhando com JSON:**

### Exemplo de Requisição Ajax que Retorna JSON:

```python
<!-- HTML -->
<button id="loadJsonData">Carregar JSON</button>
<div id="jsonOutput"></div>

<!-- JavaScript -->
<script>
  document.getElementById("loadJsonData").addEventListener("click", function() {
    fetch("https://api.example.com/json-data")
      .then(response => response.json())
      .then(data => {
        document.getElementById("jsonOutput").innerHTML = data.message;
      })
      .catch(error => console.error("Erro ao carregar JSON:", error));
  });
</script>
```

****Promessas e Callbacks:****

```python
function fetchData(callback) {
  setTimeout(function() {
    var data = "Dados recuperados da fonte externa";
    callback(data);
  }, 1000);
}

fetchData(function(result) {
  console.log(result);
});
```

**Uso de Promessas:**

1. **fetchData():** Função que retorna uma Promise, simulando uma operação assíncrona com **`setTimeout`**. Se a operação for bem-sucedida, ela chama **`resolve`** com os dados recuperados; se falhar, chama **`reject`** com uma mensagem de erro.
2. **Chamada de fetchData():** Chama a função **`fetchData()`**, que retorna uma Promise.
3. **Manipulação do Resultado:** O método **`then`** é usado para manipular o resultado bem-sucedido da Promise. No exemplo, imprime os dados recuperados no console.
4. **Manipulação de Erro:** O método **`catch`** é usado para manipular qualquer erro que ocorra durante a execução da Promise. No exemplo, imprime a mensagem de erro no console.

```python
// Definição de uma função que retorna uma Promise
function fetchData() {
  return new Promise(function(resolve, reject) {
    // Emula uma operação assíncrona (pode ser uma requisição AJAX, por exemplo)
    setTimeout(function() {
      // Indica se a operação foi bem-sucedida
      var success = true;

      // Se a operação foi bem-sucedida, chama o resolve com os dados
      if (success) {
        var data = "Dados recuperados da fonte externa";
        resolve(data);
      } else {
        // Se a operação falhou, chama o reject com uma mensagem de erro
        reject("Erro ao recuperar dados");
      }
    }, 1000); // Simula uma operação que leva 1 segundo para ser concluída
  });
}

// Chama a função fetchData, que retorna uma Promise
fetchData()
  // Manipula o resultado bem-sucedido usando o método then
  .then(function(result) {
    console.log(result); // Exibe os dados recuperados no console
  })
  // Manipula um erro usando o método catch
  .catch(function(error) {
    console.error(error); // Exibe a mensagem de erro no console
  });
```

### **Exemplo básico com Ajax:**

****Requisição GET com jQuery:****

```python
<!-- HTML -->
<!-- Botão para carregar dados -->
<button id="loadData">Carregar Dados</button>

<!-- Div para exibir os dados carregados -->
<div id="output"></div>

<!-- jQuery -->
<!-- Inclusão da biblioteca jQuery -->
<script src="https://code.jquery.com/jquery-3.6.4.min.js"></script>

<script>
  // Aguarda o documento HTML ser completamente carregado
  $(document).ready(function() {
    // Adiciona um ouvinte de evento ao botão com id "loadData"
    $("#loadData").click(function() {
      // Realiza uma requisição AJAX usando jQuery
      $.ajax({
        // URL para a qual a requisição é feita
        url: "https://api.example.com/data",
        
        // Tipo de requisição (GET neste caso)
        type: "GET",

        // Tipo de dados esperado na resposta (JSON neste caso)
        dataType: "json",

        // Função chamada em caso de sucesso na requisição
        success: function(data) {
          // Atualiza o conteúdo da div com id "output" com a mensagem recebida
          $("#output").html(data.message);
        },

        // Função chamada em caso de erro na requisição
        error: function(error) {
          // Exibe no console uma mensagem de erro
          console.error("Erro ao carregar dados:", error);
        }
      });
    });
  });
</script>
```

****Requisição POST com jQuery:****

```python
<!-- HTML -->
<!-- Botão para enviar dados -->
<button id="postData">Enviar Dados</button>

<!-- Div para exibir a resposta do envio de dados -->
<div id="postOutput"></div>

<!-- jQuery -->
<!-- Inclusão da biblioteca jQuery -->
<script src="https://code.jquery.com/jquery-3.6.4.min.js"></script>

<script>
  // Aguarda o documento HTML ser completamente carregado
  $(document).ready(function() {
    // Adiciona um ouvinte de evento ao botão com id "postData"
    $("#postData").click(function() {
      // Define os dados a serem enviados no formato de um objeto
      var dataToSend = {
        key1: "value1",
        key2: "value2"
      };

      // Realiza uma requisição AJAX usando jQuery
      $.ajax({
        // URL para a qual a requisição é feita
        url: "https://api.example.com/post-endpoint",

        // Tipo de requisição (POST neste caso)
        type: "POST",

        // Tipo de conteúdo enviado na requisição (JSON neste caso)
        contentType: "application/json",

        // Dados a serem enviados convertidos para JSON
        data: JSON.stringify(dataToSend),

        // Função chamada em caso de sucesso na requisição
        success: function(data) {
          // Atualiza o conteúdo da div com id "postOutput" com a mensagem recebida
          $("#postOutput").html(data.message);
        },

        // Função chamada em caso de erro na requisição
        error: function(error) {
          // Exibe no console uma mensagem de erro
          console.error("Erro ao enviar dados:", error);
        }
      });
    });
  });
</script>
```

Esses são exemplos básicos. Note que **`$.ajax()`** fornece muitas opções, como **`beforeSend`**, **`complete`**, etc., que podem ser usadas para manipular diferentes estágios da requisição. O uso de métodos como **`$.get()`**, **`$.post()`**, **`$.getJSON()`** é mais específico para certos tipos de requisições, simplificando ainda mais o código em casos mais simples.