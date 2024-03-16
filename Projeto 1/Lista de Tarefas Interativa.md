# Projeto 1: Lista de Tarefas Interativa

Este projeto envolve a criação de uma lista de tarefas interativa usando HTML, CSS e JavaScript. Ele abordará conceitos básicos de manipulação do DOM, eventos e armazenamento local.

**Funcionalidades:**

- Adicionar tarefas à lista.
- Marcar tarefas como concluídas.
- Remover tarefas da lista.
- Armazenar as tarefas localmente para persistência de dados.

**index.html**

```python
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link rel="stylesheet" href="styles.css">
  <title>Lista de Tarefas</title>
</head>
<body>
  <div class="container">
    <h1>Lista de Tarefas</h1>
    <div>
      <input type="text" id="taskInput" placeholder="Adicione uma tarefa">
      <button id="addTaskBtn">Adicionar</button>
    </div>
    <ul id="taskList"></ul>
  </div>
  <script src="https://code.jquery.com/jquery-3.6.4.min.js"></script>
  <script src="script.js"></script>
</body>
</html>
```

css

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
}

button {
  padding: 8px;
  cursor: pointer;
}

li {
  list-style-type: none;
  margin: 10px 0;
  padding: 10px;
  background-color: #fff;
  border: 1px solid #ddd;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.completed {
  text-decoration: line-through;
  color: #888;
}
```

scripts.js

```python
$(document).ready(function () {
  // Carregar tarefas salvas localmente
  loadTasks();

  // Adicionar tarefa
  $('#addTaskBtn').on('click', function () {
    var taskText = $('#taskInput').val();
    if (taskText.trim() !== '') {
      addTask(taskText);
      saveTasks();
      $('#taskInput').val('');
    }
  });

  // Marcar/desmarcar tarefa como concluída
  $(document).on('click', 'li', function () {
    $(this).toggleClass('completed');
    saveTasks();
  });

  // Remover tarefa
  $(document).on('click', 'span', function (e) {
    e.stopPropagation(); // Evitar a propagação do evento para o elemento pai (li)
    $(this).parent().fadeOut(500, function () {
      $(this).remove();
      saveTasks();
    });
  });

  // Função para adicionar tarefa
  function addTask(text) {
    $('#taskList').append('<li><span>&times;</span>' + text + '</li>');
  }

  // Função para carregar tarefas salvas localmente
  function loadTasks() {
    var tasks = localStorage.getItem('tasks');
    if (tasks) {
      $('#taskList').html(tasks);
    }
  }

  // Função para salvar tarefas localmente
  function saveTasks() {
    var tasks = $('#taskList').html();
    localStorage.setItem('tasks', tasks);
  }
});
```