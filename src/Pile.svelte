<script>
  import Card from "./Card.svelte";

  export let cards = [];
</script>

<div class="pile">
  {#each cards as card, index (card.key)}
    <Card 
      suit={card.suit} 
      value={card.value} 
      visable={card.visable}
      bottomCard={index === 0} />
  {/each}
</div>
