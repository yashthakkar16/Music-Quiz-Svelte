<script>
  import { fade } from "svelte/transition";
   import Question from "./Question.svelte";
   import Modal from "./Modal.svelte";
   import  {score}from "./store.js";
    let quiz = getQuiz();
    let activeQuestion = 0;
    
    let isModalOpen = false;

   
    function nextQuestion() {
        activeQuestion+=1
    }

    
  function resetQuiz() {
   isModalOpen = false;
    score.set(0);
    activeQuestion = 0
    quiz = getQuiz();
  }

 

    async function getQuiz() {
        const rez = await fetch('https://opentdb.com/api.php?amount=10&category=12&difficulty=easy&type=multiple');
        const quiz = await rez.json();
        return quiz;
        
    }

    $: if (activeQuestion > 9) {
      isModalOpen = true;
    }
 
</script>
<style>
  button{
      cursor: pointer;
      background-color: #524763;
      color: white;
  }
  .fade-wrapper{
    position: absolute;
  }
 
  .container {
    min-height: 370px;
    
  }


</style>

<div>
    
    <h3>My Score : {$score}</h3>
    <h3>Question #{activeQuestion + 1}</h3>
    <!-- {#if activeQuestion>9}
    
    <button on:click={resetQuiz}>Start Quiz</button>
    {/if} -->
   
  <div class="container">
  {#await quiz}
     Loading..
  {:then data}
  {#each data.results as question , index}
    {#if index === activeQuestion}
    <div transition:fade class="fade-wrapper">
        <Question  {question} {nextQuestion}/>
    </div>
      {/if}
    {/each}
{/await}
</div>         
</div>
{#if isModalOpen}
  <Modal on:close={resetQuiz}>
    <h2>You won! Congratulations 🙌</h2>
    <h4>Your Score: {$score}</h4>
    <button on:click={resetQuiz}>Start Over</button>
  </Modal>
{/if}
