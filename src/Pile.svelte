<script>
  import { createEventDispatcher } from 'svelte';
  import Card from './Card.svelte';

  export let pile = [];

  const dispatch = createEventDispatcher();

  const isBlackSuit = suit => {
    return suit === 'club' || suit === 'spade';
  }

  const isRedSuit = suit => {
    return suit === 'diamond' || suit === 'heart';
  }

  const isValidDrop = (pile, dropCard) => {
    const topCard = pile.cards[pile.cards.length - 1];
    return topCard.value === dropCard.value + 1 && isValidSuit(topCard, dropCard);
  }

  const isValidSuit = (topCard, dropCard) => {
    return isBlackSuit(topCard.suit)
      ? isRedSuit(dropCard.suit)
      : isBlackSuit(dropCard.suit);
  }

  const onAddCard = event => {
    const dropCard = event.detail;

    if (isValidDrop(pile, dropCard)) {
      let updatedPile = JSON.parse(JSON.stringify(pile));
      updatedPile.cards.push(dropCard);
      dispatch('updateDraggedToPile', updatedPile);
    } else {
      console.log('nope!');
    }
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
