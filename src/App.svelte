<script lang="ts">
  import Header from '@/lib/Header.svelte'
  import AddNewNote from '@/lib/AddNewNote.svelte'
  import Note from '@/lib/Note.svelte'
  import type { INote } from './models/INote'
  import EditNoteModal from './lib/EditNoteModal.svelte'

  let notes = [
    {
      id: 1,
      title: 'Some Note',
      content: 'This note is about this and that',
      date: '2021/11/29',
      isFavorite: false,
      tags: ['test', 'text'],
    },
    {
      id: 2,
      title: 'Another Note',
      content: 'This is yet another note about this and that',
      date: '2021/11/29',
      isFavorite: true,
      tags: ['test', 'text', 'extra'],
    },
  ]

  let showEditModal = false
  let noteToEdit: INote

  const openEditNote = (note?: INote) => {
    showEditModal = true
    noteToEdit = note
  }

  const closeEditModal = () => {
    showEditModal = false
    noteToEdit = null
  }

  const saveNote = (event: CustomEvent) => {
    const note = event.detail as INote
    const isEditedNote = notes.find(n => n.id === note.id)
    if (isEditedNote) {
      notes = notes.map(n => (n.id === note.id ? note : n))
    } else {
      notes = [...notes, note]
    }
  }

  const deleteNote = (event: CustomEvent) => {
    const id = event.detail as number
    notes = notes.filter(n => n.id === id)
  }

  const toggleFavorite = (event: CustomEvent) => {
    const id = event.detail as number
    notes = notes.map(n =>
      n.id === id ? { ...n, isFavorite: !n.isFavorite } : n
    )
  }
</script>

<Header />

<main>
  <div class="notes">
    <AddNewNote on:click={openEditNote} />
    {#each notes as note}
      <Note
        {note}
        on:click={() => openEditNote(note)}
        on:toggleFavorite={toggleFavorite}
      />
    {/each}
    {#if showEditModal}
      <EditNoteModal
        note={noteToEdit}
        on:save={saveNote}
        on:delete={deleteNote}
        on:close={closeEditModal}
      />
    {/if}
  </div>
</main>

<style>
  :root {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen,
      Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  }

  :global(*) {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  main {
    text-align: center;
  }

  .notes {
    display: flex;
    justify-content: space-around;
    margin: 20px;
  }
</style>
