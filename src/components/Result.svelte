<script>
    export let questionsList;

    let score = 0;
    questionsList.forEach(q => {
        if (q.isCorrect) {
            score++;
        }
    })
</script>

<h1>Résultat du Quiz</h1>
<h2>{score} / {questionsList.length}</h2>
<ul>
    {#each questionsList as element}
        <li class="wrapper">
            <h4>{element.question}</h4>
            <ul>
                {#each element.options as option, optionIndex}
                    <li
                        class:correct={element.isCorrect &&
                            optionIndex === element.correctAnswer}
                        class:incorrect={!element.isCorrect &&
                            optionIndex === element.userAnswer}
                    >
                        {option}
                    </li>
                {/each}
            </ul>
        </li>
    {/each}
</ul>

<style>
    /* ... Styles spécifiques à ce composant */
    .wrapper {
        border: .1rem solid #4b4b4b;
        border-radius: 5px;
        margin-bottom: 1rem;
        padding: 1rem;
        width: 40rem;
    }
    ul {
        display: flex;
        flex-direction: column;
        align-items: center;
        padding: 0;
    }
    li {
        list-style: none;
        width: 70%;
    }
    .correct {
        background-color: lightgreen;
    }

    .incorrect {
        background-color: lightcoral;
    }
</style>
