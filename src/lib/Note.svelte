<script lang="ts">
  import { createEventDispatcher } from 'svelte'

  export let id: number
  export let title: string
  export let content: string
  export let date: string
  export let isFavorite: boolean
  export let tags: string[]

  const dispatch = createEventDispatcher()

  const toggleFav = (e: Event) => {
    e.stopPropagation()
    dispatch('toggleFavorite', id)
  }
</script>

<div class="note" on:click={toggleFav}>
  <div class="top">
    <h2>{title}</h2>
    <p>{content.length > 50 ? content.substr(0, 50) + '...' : content}</p>
  </div>
  <div class="bottom">
    <div class="note-tags">
      {#each tags as tag}
        <span class="tag">{tag}</span>
      {/each}
    </div>
    <div class="note-footer">
      <span>{date}</span>
      <span on:click={toggleFav} class={`star ${isFavorite ? 'fav' : ''}`}
        >{isFavorite ? '★' : '☆'}</span
      >
    </div>
  </div>
</div>

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
