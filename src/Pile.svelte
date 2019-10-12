<script>
  import Card from "./Card.svelte";

  export let cards = [];
</script>

<div class="pile">
  {#each cards as card (card.key)}
    <Card suit={card.suit} value={card.value} visable={card.visable} />
  {/each}
</div>
