<script>
    export let questionsList;
    export let currentQuestionIndex;
    export let goToNextQuestion;
    export let goToPreviousQuestion;
    export let showQuizResult;

    let selectedOption = null;

    function selectAnswer(optionIndex) {
        selectedOption = optionIndex;
    }

    function validateAnswer() {
        const currentQuestion = questionsList[currentQuestionIndex];
        currentQuestion.userAnswer = selectedOption;
        currentQuestion.isCorrect =
            selectedOption === currentQuestion.correctAnswer;
            console.log(questionsList);
    }

    async function previousQuestion() {
        await goToPreviousQuestion();
        // console.log(questionsList[currentQuestionIndex].isCorrect);
        // console.log(questionsList[currentQuestionIndex].userAnswer);
        // console.log(questionsList[currentQuestionIndex].isCorrect);
        selectedOption = questionsList[currentQuestionIndex].userAnswer;
        
    }
    async function nextQuestion() {
        await goToNextQuestion();
        if (questionsList[currentQuestionIndex].userAnswer) {
            selectedOption = questionsList[currentQuestionIndex].userAnswer;
        }
        else {
            selectedOption = null;
        }
    }
</script>

<div>
    <h3>{questionsList[currentQuestionIndex].question}</h3>
    <ul>
        {#each questionsList[currentQuestionIndex].options as option, optionIndex}
            <li
                class:selected={selectedOption === optionIndex}
                
                on:click={() => selectAnswer(optionIndex)}
                on:keypress={() => selectAnswer(optionIndex)}
            >
                {option}
            </li>
        {/each}
    </ul>
    <button on:click={validateAnswer} disabled={selectedOption === null}> Valider </button>


    <button
        on:click={previousQuestion}
        disabled={currentQuestionIndex === 0}
    >
        Question précédente
    </button>

    <button
        on:click={nextQuestion}
        disabled={currentQuestionIndex === questionsList.length - 1}
    >
        Question suivante
    </button>

    {#if currentQuestionIndex === questionsList.length - 1}
        <button on:click={showQuizResult}
            disabled={selectedOption === null}>
            Voir le résultat
        </button>
    {/if}
</div>

<style>
    /* ... Styles spécifiques à ce composant */
    ul {
        padding: 0;
    }
    li {
        list-style: none;
    }
    .selected {
        background-color: lightblue;
    }
    /* .correct {
        background-color: lightgreen;
    }
    .incorrect {
        background-color: lightcoral;
    } */
</style>
