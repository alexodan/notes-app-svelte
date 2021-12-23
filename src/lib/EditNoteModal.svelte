<script script lang="ts">
  import Modal from '@/lib/Modal.svelte'
  import type { INote } from 'src/models/INote'
  import { createEventDispatcher } from 'svelte'

  export let note: INote
  let textarea: HTMLElement

  const onInput = () => {
    if (textarea) {
      textarea.style.height = 'auto'
      textarea.style.height = `${textarea.scrollHeight}px`
    }
  }

  const dispatch = createEventDispatcher()
</script>

<Modal on:closeModal={() => dispatch('close')}>
  <div slot="title" class="title">Edit Note</div>
  <div slot="body" class="modal-body">
    <label class="label" for="note-title">Title:</label>
    <input bind:value={note.title} id="note-title" class="input" type="text" />

    <label class="label" for="note-tags">Tags:</label>
    <!-- <input bind:value={tagString}  id="note-tags" class="input" type="text" /> -->

    <label class="label" for="note-content">Content:</label>
    <textarea
      id="note-content"
      bind:this={textarea}
      bind:value={note.content}
      class="input"
      type="textarea"
      on:input={onInput}
    />

    {#if note.date}
      <div class="label">Last Updated:</div>
      <div class="text">{note.date}</div>
    {/if}
  </div></Modal
>

<style>
  .modal-body {
    width: 700px;
    padding: 20px 15px 10px;
    display: grid;
    grid-template-columns: 1fr 3fr;
    gap: 15px 0;
  }
  .label {
    grid-column: 1;
    line-height: 30px;
  }
  .input {
    grid-column: 2;
    height: 30px;
    border-radius: 5px;
    border: 1px solid #c3c3c3;
  }
  .text {
    height: 30px;
    color: #808080;
    display: flex;
    align-items: center;
  }
  .modal-footer {
    padding: 0 15px;
    display: grid;
    grid-template-columns: 1fr 1fr;
  }

  .buttons-wrapper {
    text-align: right;
  }
  .button {
    height: 30px;
    padding: 0 10px;
    text-align: center;
    box-sizing: content-box;
    border-radius: 3px;
    border: 1px solid #000;
  }
  .button:active {
    background-color: #b9b7b7;
  }
  .button .save {
    background-color: #1dbd73;
    color: #fff;
  }
  .button .save:active {
    background-color: #1a8e56;
  }
  .disabled {
    opacity: 0.5;
  }
  .delete {
    background-color: #e81414;
    color: #fff;
  }

  #note-content {
    resize: vertical;
    height: fit-content;
    min-height: 30px;
  }
</style>
