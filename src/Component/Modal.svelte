<script>
    import { fly, fade } from "svelte/transition";
    import { createEventDispatcher } from "svelte";
    let w;
    const dispatch = createEventDispatcher();
  </script>
  
  <style >
    .modal-bg {
      position: fixed;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      background: rgba(0, 0, 0, 0.8);
      display: flex;
      justify-content: center;
      align-items: center;
      
     
    }
    .modal {
      background: white;
      padding: 20px;
      border-radius: 15px;
      width: 50%;
      height: 50%;
    }
    .fas{
      cursor: pointer;
      border: none;
    }
   
  </style>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta2/css/all.min.css" integrity="sha512-YWzhKL2whUzgiheMoBFwW8CKV4qpHQAEuvilg9FAn5VJUDwKZZxkJNuGM4XkWuk94WCrrwslk8yWNGmY1EduTA==" crossorigin="anonymous" referrerpolicy="no-referrer" />

  
  <div class="modal-bg" transition:fade bind:clientWidth={w}>
    <div class="modal" transition:fly={{ y: -100 }}>
      <button
        on:click={() => {
          dispatch('close');
        }}><i class="fas fa-window-close"></i>

      </button>
      <!-- <slot>optional fallback</slot> -->
      <slot />
      <!-- <slot name="modal" /> -->
    </div>
  </div>
  