<script>
    import {score} from "./store.js";
    export let question;
    export let nextQuestion;
    
    

    let isCorrect;
    let isAnswered = false;
    let answers = question.incorrect_answers.map(answer=>{
        return {
            answer,
            correct:false
        }
    });

    let allAnswer = [...answers, {
        answer: question.correct_answer,
        correct: true
    }
    ]
    shuffle(allAnswer);

    function shuffle(array) {
        array.sort(() => Math.random()- 0.5);
    }

    function checkQuestion(correct) {
    if (!isAnswered) {
      isAnswered = true;
      isCorrect = correct;
      if (correct) {
        score.update(val => val+1 )
      }
    }
  }

</script>

<style>
  h5 {
    color: blueviolet;
  }

  h5.wrong {
    color: red;
  }

  h5.isCorrect {
    color: green;
  }
  .answer {
    /* display: block; */
    display: inline;
    margin-right: 8px;
    
  }
  button{
    background-color: #524763;
    color: white;
    cursor: pointer;
    border-radius: 10px;
  }
  button:hover{
    background-color: rgb(163, 138, 197);
    color: black;
  }

  @media only screen and (max-width: 608px) {

  .answer {
    display: block;
    /* display: inline; */
    margin-right: 8px;
    
  }
}
</style>
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta2/css/all.min.css" 
integrity="sha512-YWzhKL2whUzgiheMoBFwW8CKV4qpHQAEuvilg9FAn5VJUDwKZZxkJNuGM4XkWuk94WCrrwslk8yWNGmY1EduTA==" 
crossorigin="anonymous" referrerpolicy="no-referrer" />

<h3>{@html question.question}</h3>
{#if isAnswered}
  <h5 class:isCorrect class:wrong={!isCorrect}>
    {#if isCorrect}You got it right{:else}You goofed up{/if}
  </h5>
{/if}
{#each allAnswer as answer}

<button class="answer" disabled={isAnswered} on:click={() => checkQuestion(answer.correct)}>
    {@html answer.answer}
  </button> 
{/each}

{#if isAnswered}
<br>
<button on:click={nextQuestion}><i class="fas fa-arrow-right"></i></button>
{/if} 