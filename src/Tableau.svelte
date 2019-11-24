<script>
  import Pile from './Pile.svelte';

  export let tableau;
</script>

<section class="tableau">
  {#each tableau as pile}
    <Pile {pile} on:updateDraggedToPile on:updateDraggedFromPile />
  {/each}
</section>

<style>
  .tableau {
    grid-area: tableau;
    display: grid;
    grid-template-columns: repeat(7, 100px);
    padding: 8px 16px;
  }
</style>
