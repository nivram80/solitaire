<script>
  import { createEventDispatcher } from 'svelte';
  import Card from './Card.svelte';

  const dispatch = createEventDispatcher();

  export let pile = [];

  const onAddCard = event => {
    const card = event.detail;
    let updatedPile = JSON.parse(JSON.stringify(pile));
    updatedPile.cards.push(card);
    dispatch('updateDraggedToPile', updatedPile);
  };

  const onRemoveCard = () => {
    let updatedPile = JSON.parse(JSON.stringify(pile));
    updatedPile.cards.pop();
    dispatch('updateDraggedFromPile', updatedPile);
  };
</script>

<div class="pile">
  {#each pile.cards as card, index (card.key)}
    <Card
      {card}
      bottomCard={index === 0}
      topCard={index === pile.cards.length - 1}
      on:addCard={onAddCard}
      on:removeCard={onRemoveCard} />
  {/each}
</div>
