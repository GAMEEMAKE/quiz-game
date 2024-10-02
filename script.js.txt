const questions = [
    {
        question: "Hangi etken madde ağrı kesici olarak kullanılır?",
        options: ["Paracetamol", "Ibuprofen", "Aspirin", "Tüm seçenekler"],
        answer: 3 // Tüm seçenekler doğru
    },
    {
        question: "Aspirin hangi hastalığın tedavisinde kullanılır?",
        options: ["Yüksek tansiyon", "Ateş", "Baş ağrısı", "Kalp hastalıkları"],
        answer: 3
    },
    {
        question: "Hangisi antihistaminik bir ilaçtır?",
        options: ["Loratadin", "Amoksisilin", "Metformini", "Aspirin"],
        answer: 0 // Loratadin doğru
    },
    {
        question: "Antibiyotiklerin amacı nedir?",
        options: ["Ağrıyı kesmek", "Bakteriyel enfeksiyonları tedavi etmek", "Viral enfeksiyonları tedavi etmek", "Ateşi düşürmek"],
        answer: 1
    },
    {
        question: "Hangisi antidepresan bir ilaçtır?",
        options: ["Fluoksetin", "Ibuprofen", "Paracetamol", "Klorokin"],
        answer: 0 // Fluoksetin doğru
    },
];

let currentQuestionIndex = 0;
let score = 0;

function displayQuestion() {
    const questionContainer = document.getElementById("question");
    const optionsContainer = document.getElementById("options");
    const currentQuestion = questions[currentQuestionIndex];

    questionContainer.innerText = currentQuestion.question;
    optionsContainer.innerHTML = ""; // Önceki seçenekleri temizle

    currentQuestion.options.forEach((option, index) => {
        const button = document.createElement("button");
        button.innerText = option;
        button.onclick = () => selectOption(index);
        optionsContainer.appendChild(button);
    });
}

function selectOption(index) {
    if (index === questions[currentQuestionIndex].answer) {
        score++;
    }
    currentQuestionIndex++;
    if (currentQuestionIndex < questions.length) {
        displayQuestion();
    } else {
        showResult();
    }
}

function showResult() {
    const quizContainer = document.getElementById("quiz-container");
    const resultContainer = document.getElementById("result");
    const scoreDisplay = document.getElementById("score");

    quizContainer.classList.add("hidden");
    resultContainer.classList.remove("hidden");
    scoreDisplay.innerText = `Skorunuz: ${score} / ${questions.length}`;
}

function restartQuiz() {
    currentQuestionIndex = 0;
    score = 0;
    document.getElementById("quiz-container").classList.remove("hidden");
    document.getElementById("result").classList.add("hidden");
    displayQuestion();
}

// Sayfa yüklendiğinde ilk soruyu göster
displayQuestion();
