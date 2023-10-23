<script>
  import Note from './Note.svelte';

  let notes = [
    {
      id: 1,
      text: 'Welcome here'
    },
    {
      id: 2,
      text: 'Hey there'
    }
  ];
</script>

<div class="notes-container">
  {#each notes as note (note.id)}
    <Note>
      <div contenteditable>{note.text}</div>
    </Note>
  {/each}
</div>

<style>
  .notes-container {
    display: flex;
    justify-content: space-around;
		color:black;
  }
</style>

