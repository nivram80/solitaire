<script>
  import Card from "./Card.svelte";

  export let cards = [];
</script>

<style>
	.pile {
		width: 120px;
		border: 1px solid black;
	}
</style>

<div class="pile">
  {#each cards as card (card.key)}
    <Card suit={card.suit} value={card.value} />
  {/each}
</div>
