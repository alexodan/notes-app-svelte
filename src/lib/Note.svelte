<script lang="ts">
  import { createEventDispatcher } from 'svelte'
  import EditNodeModal from './EditNodeModal.svelte'
  import type { INote } from '../models/INote'

  export let note: INote

  let showModal = false

  const dispatch = createEventDispatcher()

  const toggleFav = (e: Event) => {
    e.stopPropagation()
    dispatch('toggleFavorite', note.id)
  }

  const toggleModal = () => (showModal = !showModal)
</script>

<div class="note" on:click={toggleModal}>
  <div class="top">
    <h2>{note.title}</h2>
    <p>
      {note.content.length > 50
        ? note.content.substr(0, 50) + '...'
        : note.content}
    </p>
  </div>
  <div class="bottom">
    <div class="note-tags">
      {#each note.tags as tag}
        <span class="tag">{tag}</span>
      {/each}
    </div>
    <div class="note-footer">
      <span>{note.date}</span>
      <span on:click={toggleFav} class={`star ${note.isFavorite ? 'fav' : ''}`}
        >{note.isFavorite ? '★' : '☆'}</span
      >
    </div>
  </div>
</div>
{#if showModal}
  <EditNodeModal {note} />
{/if}

<style>
  .note {
    /* align-items: flex-start; */
    border-radius: 10px;
    display: flex;
    box-shadow: rgba(0, 0, 0, 0.24) 0px 3px 8px;
    flex-direction: column;
    height: 250px;
    justify-content: space-between;
    padding: 15px 10px;
    width: 200px;
  }
  .top {
    text-align: left;
  }
  .top h2 {
    margin-bottom: 15px;
  }
  .bottom {
    display: flex;
    flex-direction: column;
  }
  .note-tags {
    align-self: flex-start;
  }
  .tag {
    background-color: lightgray;
    border-radius: 10px;
    padding: 3px 5px;
    margin-right: 10px;
  }
  .bottom .note-footer {
    display: flex;
    color: gray;
    justify-content: space-between;
    margin-top: 10px;
  }
  .star {
    cursor: pointer;
  }
</style>
