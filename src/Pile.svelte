<script>
  import { createEventDispatcher } from "svelte";
  import Card from "./Card.svelte";

  const dispatch = createEventDispatcher();

  export let pile = [];

  const onAddCard = event => {
    const newCard = event.detail;
    let updatedPile = JSON.parse(JSON.stringify(pile));
    updatedPile.cards.push(newCard);;
    dispatch("updatePile", updatedPile);
  }
</script>

<div class="pile">
  {#each pile.cards as card, index (card.key)}
    <Card 
      card={card}
      bottomCard={index === 0}
      topCard={index === pile.cards.length - 1}
      on:addCard={onAddCard} />
  {/each}
</div>
