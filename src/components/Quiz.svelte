<script>
    import { onMount } from "svelte";
    import { questionsList } from "../data/Data.js";
    import Question from "./Question.svelte";
    import Result from "./Result.svelte";

    let currentQuestionIndex = 0;
    let showResult = false;

    function goToNextQuestion() {
        currentQuestionIndex++;
    }

    function goToPreviousQuestion() {
        currentQuestionIndex--;
        // console.log(questionsList[currentQuestionIndex].isCorrect);
        
    }

    function showQuizResult() {
        showResult = true;
    }

    let initialized = false;

    onMount(() => {
        if (!initialized) {
            questionsList.forEach((question) => {
                question.userAnswer = null;
                question.isCorrect = false;
            });
            initialized = true;
        }
    });
</script>

<main>
    {#if !showResult}
        <h1>Quiz</h1>
        <Question
            {questionsList}
            {currentQuestionIndex}
            {goToNextQuestion}
            {goToPreviousQuestion}
            {showQuizResult}
        />
    {:else}
        <Result {questionsList} />
        <button on:click={() => showResult = false}>Améliorer votre score</button>
    {/if}
</main>

<style>
    /* ... Styles */
</style>
