**Projeto 10: Quiz**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Quiz Interativo</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <div id="quiz-container">
        <h1>Quiz Interativo</h1>
        <div id="question-container">
            <!-- Perguntas e opções de resposta serão inseridas aqui dinamicamente com jQuery -->
        </div>
        <button id="submit-btn">Enviar Respostas</button>
        <div id="result-container"></div>
    </div>

    <script src="https://code.jquery.com/jquery-3.6.4.min.js"></script>
    <script src="script.js"></script>
</body>
</html>
```

```css
body {
  font-family: 'Arial', sans-serif;
  text-align: center;
  margin: 20px;
}

#quiz-container {
  max-width: 600px;
  margin: auto;
  border: 1px solid #ccc;
  padding: 20px;
  border-radius: 8px;
}

button {
  background-color: #4CAF50;
  color: white;
  padding: 10px 20px;
  font-size: 16px;
  cursor: pointer;
  border: none;
  border-radius: 4px;
}

button:hover {
  background-color: #45a049;
}

#result-container {
  margin-top: 20px;
  font-weight: bold;
}
```

```jsx
$(document).ready(function() {
    const questions = [
        {
            question: 'Qual é a capital da França?',
            options: ['Londres', 'Paris', 'Berlim', 'Madrid'],
            correctAnswer: 'Paris'
        },
        {
            question: 'Quanto é 2 + 2?',
            options: ['3', '4', '5', '6'],
            correctAnswer: '4'
        },
        {
            question: 'Quem escreveu "Romeu e Julieta"?',
            options: ['Charles Dickens', 'William Shakespeare', 'Jane Austen', 'F. Scott Fitzgerald'],
            correctAnswer: 'William Shakespeare'
        }
    ];

    const quizContainer = $('#question-container');
    const resultContainer = $('#result-container');
    const submitButton = $('#submit-btn');

    // Inicializar o Quiz
    function initQuiz() {
        for (let i = 0; i < questions.length; i++) {
            const questionHTML = `
                <div class="question" id="question${i}">
                    <p>${questions[i].question}</p>
                    ${generateOptions(questions[i].options, i)}
                </div>
            `;
            quizContainer.append(questionHTML);
        }
    }

    // Gerar opções de resposta
    function generateOptions(options, questionIndex) {
        let optionsHTML = '';
        for (let i = 0; i < options.length; i++) {
            optionsHTML += `
                <label>
                    <input type="radio" name="q${questionIndex}" value="${options[i]}"> ${options[i]}
                </label>
            `;
        }
        return optionsHTML;
    }

    // Verificar respostas ao clicar em "Enviar Respostas"
    submitButton.click(function() {
        let score = 0;

        for (let i = 0; i < questions.length; i++) {
            const selectedOption = $(`input[name=q${i}]:checked`).val();

            if (selectedOption === questions[i].correctAnswer) {
                score++;
                $(`#question${i}`).css('color', 'green');
            } else {
                $(`#question${i}`).css('color', 'red');
            }
        }

        const resultText = `Você acertou ${score} de ${questions.length} perguntas!`;
        resultContainer.text(resultText);
    });

    // Inicializar o Quiz ao carregar a página
    initQuiz();
});
```

## Com Steps para ficar melhor.

```python
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Quiz Interativo</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <div id="quiz-container">
        <h1>Quiz Interativo</h1>
        
        <div id="question-container"></div>

        <button id="next-btn">Próxima Pergunta</button>

        <button id="submit-btn">Finalizar Quiz</button>

        <div id="result-container"></div>
    </div>

    <script src="https://code.jquery.com/jquery-3.6.4.min.js"></script>
    <script src="script.js"></script>
</body>
</html>
```

```python
body {
  font-family: 'Arial', sans-serif;
  text-align: center;
  margin: 20px;
}

#quiz-container {
  max-width: 600px;
  margin: auto;
  border: 1px solid #ccc;
  padding: 20px;
  border-radius: 8px;
}

button {
  background-color: #4CAF50;
  color: white;
  padding: 10px 20px;
  font-size: 16px;
  cursor: pointer;
  border: none;
  border-radius: 4px;
}

button:hover {
  background-color: #45a049;
}

#result-container {
  margin-top: 20px;
  font-weight: bold;
}
```

```python
$(document).ready(function() {
    const questions = [
        {
            question: 'Qual é a capital da França?',
            options: ['Londres', 'Paris', 'Berlim', 'Madrid'],
            correctAnswer: 'Paris'
        },
        {
            question: 'Quanto é 2 + 2?',
            options: ['3', '4', '5', '6'],
            correctAnswer: '4'
        },
        {
            question: 'Quem escreveu "Romeu e Julieta"?',
            options: ['Charles Dickens', 'William Shakespeare', 'Jane Austen', 'F. Scott Fitzgerald'],
            correctAnswer: 'William Shakespeare'
        }
    ];

    const quizContainer = $('#question-container');
    const resultContainer = $('#result-container');
    const nextButton = $('#next-btn');
    const submitButton = $('#submit-btn');

    let currentQuestion = 0;
    let userAnswers = [];  // Armazenar as respostas do usuário

    // Inicializar o Quiz
    function initQuiz() {
        displayQuestion(currentQuestion);
    }

    // Exibir pergunta
    function displayQuestion(index) {
        quizContainer.empty();
        const question = questions[index];
        const questionHTML = `
            <div class="question">
                <p>${question.question}</p>
                ${generateOptions(question.options)}
            </div>
        `;
        quizContainer.append(questionHTML);
    }

    // Gerar opções de resposta
    function generateOptions(options) {
        let optionsHTML = '';
        for (let i = 0; i < options.length; i++) {
            optionsHTML += `
                <label>
                    <input type="radio" name="answer" value="${options[i]}"> ${options[i]}
                </label>
            `;
        }
        return optionsHTML;
    }

    // Evento de clique no botão "Próxima Pergunta"
    nextButton.click(function() {
        const selectedOption = $('input[name="answer"]:checked').val();
        if (selectedOption) {
            userAnswers.push(selectedOption);  // Armazenar a resposta do usuário
            currentQuestion++;
            if (currentQuestion < questions.length) {
                displayQuestion(currentQuestion);
            } else {
                showResults();
            }
        } else {
            alert('Por favor, selecione uma opção.');
        }
    });

    // Evento de clique no botão "Finalizar Quiz"
    submitButton.click(function() {
        showResults();
    });

    // Exibir resultado final
    function showResults() {
        quizContainer.hide();
        nextButton.hide();
        submitButton.hide();
        calculateScore();
    }

    // Calcular pontuação final
    function calculateScore() {
        let score = 0;
        for (let i = 0; i < questions.length; i++) {
            if (userAnswers[i] === questions[i].correctAnswer) {
                score++;
            }
        }
        const resultText = `Você acertou ${score} de ${questions.length} perguntas!`;
        resultContainer.text(resultText);
        resultContainer.show();
    }

    // Inicializar o Quiz ao carregar a página
    initQuiz();
});
```