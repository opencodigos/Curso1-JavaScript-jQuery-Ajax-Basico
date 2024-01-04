# JavaScript (JS): Sintaxe Básica

### **Variáveis e Tipos de Dados:**

Em JavaScript, as variáveis são utilizadas para armazenar dados. A declaração de uma variável pode ser feita usando as palavras-chave **`var`**, **`let`** ou **`const`**. Os tipos de dados mais comuns são **`string`** (texto), **`number`** (número), e **`boolean`** (verdadeiro ou falso).

**`var`** 
As variáveis declaradas com **`var`** têm escopo de função. Isso significa que são visíveis em toda a função em que são declaradas, independentemente de onde estejam no código.

```python
function exemploVar() {
    if (true) {
        var x = 10;
        console.log(x); // 10
    }
    console.log(x); // 10
}
```

**`let`** 

As variáveis declaradas com **`let`** têm escopo de bloco, o que significa que são visíveis apenas dentro do bloco em que são declaradas (dentro de uma instrução **`if`**, **`for`**, **`while`**, etc.).

```python
function exemploLet() {
    if (true) {
        let y = 20;
        console.log(y); // 20
    }
    // console.log(y); // Erro! y não está definido neste escopo
}
```

**`const`** 

As variáveis declaradas com **`const`** são constantes, o que significa que não podem ser reatribuídas após a inicialização.

```python
function exemploConst() {
    const z = 30;
    // z = 40; // Erro! Não é possível reatribuir uma constante
    console.log(z); // 30
}
```

**Escolha entre `var`, `let` e `const`:**

- Use **`const`** para valores que não precisam ser reatribuídos.
- Use **`let`** quando precisar reatribuir valores.
- Evite usar **`var`** devido ao seu escopo de função e ao comportamento de hoisting, a menos que esteja trabalhando em um ambiente onde isso seja necessário (por exemplo, código legado).

**Declaração de variáveis**

```python
var nome = "João";
let idade = 25;
const isAdulto = true;

// Tipos de dados
let salario = 2500.50; // number
let cidade = "Rio de Janeiro"; // string
```

### **Estruturas de Controle de Fluxo:**

As estruturas de controle de fluxo permitem que o programa tome decisões com base em condições.

Exemplo: 

**Estrutura condicional**

```python
let temperatura = 25;

if (temperatura > 30) {
    console.log("Está muito quente!");
} else if (temperatura > 20) {
    console.log("O clima está agradável.");
} else {
    console.log("Está um pouco frio.");
}
```

Exemplo 2:

```python
let numero = 10;

if (numero > 0) {
    console.log("O número é positivo.");
} else if (numero < 0) {
    console.log("O número é negativo.");
} else {
    console.log("O número é zero.");
}
```

### **Loops:**

Os loops são utilizados para executar um bloco de código repetidamente.

Exemplo:

```python
for (let i = 0; i < 5; i++) {
    console.log("Número: " + i);
}

// Loop while
let contador = 0;
while (contador < 3) {
    console.log("Contagem: " + contador);
    contador++;
}
```

### **Funções e Escopo:**

Funções são blocos de código reutilizáveis. O escopo refere-se à visibilidade das variáveis dentro e fora de uma função.

Exemplo:

```python
function saudacao(nome) {
    return "Olá, " + nome + "!";
}

let mensagem = saudacao("Ana");
console.log(mensagem);

// Escopo
function exemploEscopo() {
    let local = "Variável local";
    console.log(local); // Visível apenas dentro da função
}

//console.log(local); // Erro! 'local' não é visível fora da função
```

# Objetos e Arrays:

**Trabalhando com Objetos e Arrays em JavaScript:**

### Objetos:

Em JavaScript, um objeto é uma estrutura de dados que permite armazenar e organizar informações relacionadas. Os objetos consistem em pares chave-valor, onde as chaves são strings que representam propriedades e os valores podem ser de qualquer tipo de dado, inclusive outros objetos.

**Exemplo:**

```python
// Criando um objeto representando uma pessoa
let pessoa = {
    nome: "Letícia",
    idade: 25,
    cidade: "São Paulo"
};

// Acessando propriedades do objeto
console.log(pessoa.nome);  // Saída: Letícia
console.log(pessoa.idade); // Saída: 25
```

### Arrays:

Os arrays são estruturas de dados que permitem armazenar múltiplos valores em uma única variável. Os elementos em um array são acessados por meio de índices, que começam do zero.

**Exemplo:**

```python
// Criando um array de frutas
let frutas = ["maçã", "banana", "uva"];

// Acessando elementos do array
console.log(frutas[0]);  // Saída: maçã
console.log(frutas[1]);  // Saída: banana
```

### Métodos de Array:

### **forEach:**

- O método **`forEach`** executa uma função para cada elemento do array.

**Exemplo:**

```python
let frutas = ["maçã", "banana", "uva"];

// Usando forEach para imprimir cada fruta
frutas.forEach(function(fruta) {
    console.log(fruta);
});
// Saída:
// maçã
// banana
// uva
```

### **map:**

- O método **`map`** cria um novo array resultante da aplicação de uma função a cada elemento do array original.

**Exemplo:**

```python
// Usando map para criar um novo array com o dobro de cada número
let numeros = [1, 2, 3];
let dobrados = numeros.map(function(numero) {
    return numero * 2;
});
console.log(dobrados);  // Saída: [2, 4, 6]
```

### **filter:**

- O método **`filter`** cria um novo array contendo apenas os elementos que satisfazem uma condição especificada.

**Exemplo:**

```python
// Usando filter para obter apenas números pares
let numeros = [1, 2, 3, 4, 5, 6];
let pares = numeros.filter(function(numero) {
    return numero % 2 === 0;
});
console.log(pares);  // Saída: [2, 4, 6]
```

Manipulação de objetos.

****Adicionando Propriedades:****

Você pode adicionar novas propriedades a um objeto usando a notação de ponto ou a notação de colchetes.

**Exemplo:**

```python
let carro = {
    modelo: "Civic",
    ano: 2020
};

// Adicionando uma nova propriedade
carro.cor = "preto";

console.log(carro);  
// Saída: { modelo: 'Civic', ano: 2020, cor: 'preto' }
```

**Atualizando Propriedades:**

Você pode atualizar o valor de uma propriedade existente atribuindo um novo valor.

**Exemplo:**

```python
// Atualizando o ano do carro
carro.ano = 2022;

console.log(carro);
// Saída: { modelo: 'Civic', ano: 2022, cor: 'preto' }
```

**Removendo Propriedades:**

Você pode remover uma propriedade de um objeto usando o operador **`delete`**.

**Exemplo:**

```python
// Removendo a propriedade 'cor'
delete carro.cor;

console.log(carro);
// Saída: { modelo: 'Civic', ano: 2022 }
```

**Iterando Através de Propriedades:**

Você pode iterar sobre as propriedades de um objeto usando loops ou métodos específicos.

**Exemplo com Loop for...in:**

```python
let carro = {
    modelo: "Civic",
    ano: 2020
};  

for (let chave in carro) {
    console.log(chave + ": " + carro[chave]);
}
// Saída:
// modelo: Civic
// ano: 2022
```

**Exemplo com Object.keys e forEach:**

```python
let carro = {
    modelo: "Civic",
    ano: 2020
}; 

Object.keys(carro).forEach(function(chave) {
    console.log(chave + ": " + carro[chave]);
});
// Saída:
// modelo: Civic
// ano: 2022
```

# ****DOM (Document Object Model):****

O DOM (Document Object Model) é uma representação hierárquica de documentos HTML e XML, que permite a interação dinâmica com a estrutura e conteúdo da página web. A manipulação do DOM em JavaScript permite selecionar elementos, modificar conteúdo, estilos e responder a eventos do usuário.

****Seleção de Elementos do HTML:****

Por ID:

```python
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Seleção de Elementos</title>
</head>
<body>

    <div id="meuElemento">Olá, Mundo!</div>

    <script>
        // Seleção por ID
        let elementoPorId = document.getElementById("meuElemento");
        console.log(elementoPorId.textContent); // Saída: Olá, Mundo!
    </script>

</body>
</html>
```

**Por Classe:**

```python
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Seleção de Elementos</title>
</head>
<body>

    <p class="paragrafo">Este é um parágrafo.</p>
    <p class="paragrafo">Este é outro parágrafo.</p>

    <script>
        // Seleção por classe
        let elementosPorClasse = document.getElementsByClassName("paragrafo");
        for (let i = 0; i < elementosPorClasse.length; i++) {
            console.log(elementosPorClasse[i].textContent);
        }
        // Saída:
        // Este é um parágrafo.
        // Este é outro parágrafo.
    </script>

</body>
</html>
```

****Manipulação de Conteúdo e Estilos:****

**Modificando Conteúdo:**

```python
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Manipulação de Conteúdo</title>
</head>
<body>

    <div id="meuElemento">Olá, Mundo!</div>

    <script>
        // Modificando conteúdo
        let elemento = document.getElementById("meuElemento");
        elemento.textContent = "Novo conteúdo!";
    </script>

</body>
</html>
```

**Modificando Estilos:**

```python
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Manipulação de Estilos</title>
</head>
<body>

    <p id="paragrafoEstilizado">Este é um parágrafo estilizado.</p>

    <script>
        // Modificando estilos
        let paragrafo = document.getElementById("paragrafoEstilizado");
        paragrafo.style.color = "blue";
        paragrafo.style.fontSize = "18px";
    </script>

</body>
</html>
```

****Eventos e Manipulação de Eventos:****

**Adicionando um Evento:**

```python
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Eventos</title>
</head>
<body>

    <button id="meuBotao">Clique-me</button>

    <script>
        // Adicionando um evento de clique
        let botao = document.getElementById("meuBotao");
        botao.addEventListener("click", function() {
            alert("Botão clicado!");
        });
    </script>

</body>
</html>
```

**Manipulando Eventos:**

```python
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Manipulação de Eventos</title>
</head>
<body>

    <input type="text" id="meuInput">
    <p id="mensagem"></p>

    <script>
        // Manipulando eventos de input
        let input = document.getElementById("meuInput");
        let mensagem = document.getElementById("mensagem");

        input.addEventListener("input", function() {
            mensagem.textContent = "Texto atual: " + input.value;
        });
    </script>

</body>
</html>
```