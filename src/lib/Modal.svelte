<script lang="ts">
  import { createEventDispatcher } from 'svelte'

  const dispatch = createEventDispatcher()
</script>

<div class="modal-wrapper">
  <div class="modal">
    <div class="modal-header">
      <slot name="title" />
      <div class="close-icon" on:click={() => dispatch('closeModal')}>x</div>
    </div>

    <slot name="body" />

    <slot name="footer" />
  </div>
</div>

<style>
  .modal-wrapper {
    position: absolute;
    top: 0;
    height: 100vh;
    width: 100vw;
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: rgb(0, 0, 0, 0.4);
  }
  .modal {
    background-color: white;
    padding: 15px 0;
    border-radius: 10px;
    box-shadow: rgb(0 0 0 / 24%) 0px 3px 8px;
  }
  .modal-header {
    display: flex;
    justify-content: space-between;
    padding: 0 15px 10px;
    border-bottom: 3px solid #e2e2e2;
  }
  .close-icon {
    cursor: pointer;
  }
</style>
