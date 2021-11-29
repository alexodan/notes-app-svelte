<script lang="ts">
  export let onAddNewNote

  const addNewNote = () => {
    // show a modal
  }
</script>

<div class="new-note" on:click={addNewNote}>
  <span>+</span>
</div>

<style>
  .new-note {
    align-items: center;
    background-color: lightgray;
    border: 5px dashed gray;
    border-radius: 10px;
    cursor: pointer;
    display: flex;
    height: 250px;
    justify-content: center;
    width: 200px;
  }
  .new-note span {
    color: gray;
    font-size: 4rem;
  }
</style>
