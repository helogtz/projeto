# projeto
Nome do Projeto: Jogo de Adivinhação de Palavras Secretas

Objetivo: O jogador tenta adivinhar uma palavra secreta em um número limitado de tentativas.

Estrutura do Projeto (Arquivos e Módulos)
Para começar, vamos dividir o código em módulos, como você pediu. Crie os seguintes arquivos (em uma pasta meu-projeto-alura):

meu-projeto-alura/
├── index.html
├── js/
│   ├── main.js
│   ├── utils.js
│   └── gameLogic.js
├── css/
│   └── style.css
Detalhamento das Etapas e Aplicação dos Conceitos
Vamos ver como cada conceito se encaixa:

1. index.html (Estrutura Básica)
Este será o arquivo principal para a interface do jogo.

HTML

<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Jogo da Palavra Secreta</title>
    <link rel="stylesheet" href="css/style.css">
</head>
<body>
    <div class="container">
        <h1>Adivinhe a Palavra Secreta!</h1>
        <p>Eu escolhi uma palavra. Tente adivinhar qual é!</p>
        <div class="word-display" id="wordDisplay">
            </div>
        <input type="text" id="guessInput" placeholder="Digite sua letra ou palavra...">
        <button id="guessButton">Adivinhar</button>
        <p id="message"></p>
        <p>Tentativas restantes: <span id="attemptsLeft"></span></p>
        <button id="resetButton" style="display: none;">Jogar Novamente</button>
    </div>

    <script type="module" src="js/main.js"></script>
</body>
</html>
2. css/style.css (Estilização - Opcional, mas bom para praticar)
Adicione um CSS básico para deixar o jogo mais apresentável.

CSS

body {
    font-family: Arial, sans-serif;
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
    background-color: #282c34;
    color: #f0f0f0;
    margin: 0;
}

.container {
    background-color: #3a404c;
    padding: 30px;
    border-radius: 10px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
    text-align: center;
    width: 90%;
    max-width: 500px;
}

h1 {
    color: #61dafb;
}

.word-display {
    font-size: 2em;
    letter-spacing: 5px;
    margin: 20px 0;
}

.word-display span {
    margin: 0 5px;
    border-bottom: 2px solid #61dafb;
    padding-bottom: 5px;
}

input[type="text"] {
    padding: 10px;
    margin: 10px 0;
    border: none;
    border-radius: 5px;
    width: calc(100% - 22px);
    background-color: #21252b;
    color: #f0f0f0;
}

button {
    background-color: #61dafb;
    color: #282c34;
    padding: 10px 20px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    font-size: 1em;
    margin-top: 10px;
}

button:hover {
    background-color: #4aa7d9;
}

#message {
    margin-top: 20px;
    font-size: 1.1em;
}
3. js/utils.js (Módulo de Utilitários)
Crie algoritmos de aleatoriedade: Aqui teremos uma função para selecionar uma palavra aleatória de uma lista.

Divida código JavaScript em módulos utilizando export: Vamos exportar a função para ser usada em outro lugar.

JavaScript

// utils.js
const words = [
    "ALURA", "PROGRAMACAO", "JAVASCRIPT", "MODULO", "FRONTEND",
    "BACKEND", "DESENVOLVIMENTO", "COMPUTADOR", "WEB", "TECNOLOGIA"
];

/**
 * Seleciona uma palavra aleatória da lista.
 * @returns {string} A palavra selecionada em letras maiúsculas.
 */
export function getRandomWord() {
    const randomIndex = Math.floor(Math.random() * words.length);
    return words[randomIndex];
}

/**
 * Aplica o conceito de fluxograma (mentalmente ou desenhando) para validar uma entrada.
 * Este método replace é um exemplo de tratamento de string.
 * @param {string} input A string de entrada para ser formatada.
 * @returns {string} A string formatada (ex: sem acentos, maiúscula).
 */
export function formatGuess(input) {
    // Conheça e aplique o método replace:
    // Remove acentos e caracteres especiais, converte para maiúsculas.
    // Primeiro, normaliza para decompor caracteres acentuados.
    // Depois, remove os diacríticos (acentos).
    // Por fim, converte para maiúsculas.
    return input
        .normalize("NFD")
        .replace(/[\u0300-\u036f]/g, "") // remove acentos
        .toUpperCase();
}
4. js/gameLogic.js (Módulo de Lógica do Jogo)
Crie condicionais no JavaScript: Para verificar se a letra ou palavra está correta, se o jogo acabou, etc.

Utilize o "for of" para criar condições de parada: Para iterar sobre a palavra secreta e a adivinhada.

Divida código JavaScript em módulos utilizando export e import: Importaremos as funções de utils.js.

JavaScript

// gameLogic.js
import { getRandomWord, formatGuess } from './utils.js';

let secretWord = '';
let maskedWord = [];
let attempts = 6; // Número de tentativas
let guessedLetters = new Set(); // Para armazenar letras já tentadas
let gameOver = false;

// Elementos do DOM
const wordDisplay = document.getElementById('wordDisplay');
const guessInput = document.getElementById('guessInput');
const message = document.getElementById('message');
const attemptsLeftSpan = document.getElementById('attemptsLeft');
const resetButton = document.getElementById('resetButton');

/**
 * Inicializa o jogo.
 */
export function initializeGame() {
    secretWord = getRandomWord();
    maskedWord = Array(secretWord.length).fill('_');
    attempts = 6;
    guessedLetters.clear();
    gameOver = false;

    updateDisplay();
    message.textContent = '';
    guessInput.value = '';
    resetButton.style.display = 'none';
    guessInput.disabled = false;
    guessInput.focus();
}

/**
 * Atualiza a exibição da palavra e das tentativas.
 */
function updateDisplay() {
    wordDisplay.innerHTML = maskedWord.map(char => `<span>${char}</span>`).join('');
    attemptsLeftSpan.textContent = attempts;
}

/**
 * Processa a tentativa do jogador.
 * @param {string} guess A letra ou palavra adivinhada pelo jogador.
 */
export function processGuess(guess) {
    if (gameOver) return;

    const formattedGuess = formatGuess(guess);

    // Validação básica da entrada
    if (!formattedGuess) {
        message.textContent = "Por favor, digite uma letra ou uma palavra.";
        return;
    }

    if (formattedGuess.length === 1) { // Adivinhou uma única letra
        if (guessedLetters.has(formattedGuess)) {
            message.textContent = `Você já tentou a letra '${formattedGuess}'.`;
            return;
        }
        guessedLetters.add(formattedGuess);

        // Crie condicionais no JavaScript:
        if (secretWord.includes(formattedGuess)) {
            message.textContent = `Boa! A letra '${formattedGuess}' está na palavra.`;
            // Atualiza a palavra mascarada
            for (let i = 0; i < secretWord.length; i++) {
                if (secretWord[i] === formattedGuess) {
                    maskedWord[i] = formattedGuess;
                }
            }
        } else {
            message.textContent = `Que pena! A letra '${formattedGuess}' não está na palavra.`;
            attempts--;
        }
    } else { // Adivinhou a palavra inteira
        // Crie condicionais no JavaScript:
        if (formattedGuess === secretWord) {
            maskedWord = secretWord.split(''); // Revela a palavra
            message.textContent = "Parabéns! Você adivinhou a palavra!";
            endGame(true);
            return;
        } else {
            message.textContent = `A palavra '${formattedGuess}' está incorreta.`;
            attempts--;
        }
    }

    updateDisplay();
    checkGameStatus();
}

/**
 * Verifica o status do jogo (vitória ou derrota).
 * Utiliza o "for of" para criar condições de parada (se todas as letras foram adivinhadas).
 */
function checkGameStatus() {
    // Verificação de vitória:
    let allLettersGuessed = true;
    for (const char of maskedWord) { // for of para iterar sobre as letras da palavra mascarada
        if (char === '_') {
            allLettersGuessed = false;
            break; // Condição de parada: se encontrar um '_' (letra não adivinhada), não precisamos continuar.
        }
    }

    if (allLettersGuessed) {
        message.textContent = "Parabéns! Você adivinhou a palavra!";
        endGame(true);
        return;
    }

    // Verificação de derrota:
    // Crie condicionais no JavaScript:
    if (attempts <= 0) {
        message.textContent = `Fim de jogo! A palavra era: ${secretWord}`;
        endGame(false);
    }
}

/**
 * Finaliza o jogo.
 * @param {boolean} won Indica se o jogador venceu.
 */
function endGame(won) {
    gameOver = true;
    guessInput.disabled = true;
    resetButton.style.display = 'block'; // Mostra o botão de reiniciar
}
5. js/main.js (Módulo Principal)
Importe os módulos: Este arquivo será o ponto de entrada e fará a ponte entre a interface e a lógica do jogo.

JavaScript

// main.js
import { initializeGame, processGuess } from './gameLogic.js';

document.addEventListener('DOMContentLoaded', () => {
    const guessInput = document.getElementById('guessInput');
    const guessButton = document.getElementById('guessButton');
    const resetButton = document.getElementById('resetButton');

    // Inicializa o jogo ao carregar a página
    initializeGame();

    // Evento de clique para o botão "Adivinhar"
    guessButton.addEventListener('click', () => {
        processGuess(guessInput.value);
        guessInput.value = ''; // Limpa o input após a tentativa
    });

    // Evento de tecla 'Enter' no input para adivinhar
    guessInput.addEventListener('keypress', (event) => {
        if (event.key === 'Enter') {
            guessButton.click(); // Simula o clique no botão
        }
    });

    // Evento de clique para o botão "Jogar Novamente"
    resetButton.addEventListener('click', () => {
        initializeGame();
    });
});
Como Rodar o Projeto
Salve todos os arquivos nas pastas correspondentes como mostrado na estrutura.

Abra o arquivo index.html no seu navegador.
