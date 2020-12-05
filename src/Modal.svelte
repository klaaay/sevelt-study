<script>
  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();

  export let showModal = false;
</script>

<style>
  .backdrop {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100vh;
    background: rgba(0, 0, 0, 0.75);
    z-index: 10;
  }

  .modal {
    position: fixed;
    top: 10vh;
    left: 10%;
    width: 80%;
    max-height: 80vh;
    background: white;
    border-radius: 5px;
    z-index: 100;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
    overflow: auto;
    padding: 20px;
  }

  header {
    border-bottom: 1px solid #ccc;
  }
</style>

<div class="backdrop" on:click={() => dispatch('cancle')} />
<div class="modal">
  <header>
    <slot name="header" />
  </header>
  <div class="content">
    <slot />
  </div>
  <footer>
    <slot name="footer">
      <button on:click={() => dispatch('close')}>close</button>
    </slot>
  </footer>
</div>
