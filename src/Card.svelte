<script>
  import { createEventDispatcher } from 'svelte';
  import Heart from './Heart.svelte';
  import Spade from './Spade.svelte';
  import Diamond from './Diamond.svelte';
  import Club from './Club.svelte';

  export let bottomCard;
  export let card;
  export let topCard;

  const dispatch = createEventDispatcher();

  const onDragover = event => {
    // console.log(event);
  };

  const onDragstart = event => {
    event.dataTransfer.setData('text/plain', JSON.stringify(card));
    // Have to wait for the browser to make a copy of the element before we remove it.
    // https://stackoverflow.com/questions/36379184/html5-draggable-hide-original-element
    setTimeout(() => {
      dispatch('removeCard', card);
    }, 1);
  };

  const onDrop = event => {
    const data = event.dataTransfer.getData('text/plain');
    dispatch('addCard', JSON.parse(data));
    event.preventDefault();
  };
</script>

<div
  class={`card ${card.suit}`}
  class:bottom-card={bottomCard}
  class:face-up={card.faceUp}
  class:top-card={topCard}
  draggable={card.faceUp}
  on:drop|preventDefault={onDrop}
  on:dragover|preventDefault={onDragover}
  on:dragstart={onDragstart}>
  {#if card.faceUp}
    <div class="card-header">
      {card.value}
      {#if card.suit === 'heart'}
        <Heart size="small" />
      {:else if card.suit === 'spade'}
        <Spade size="small" />
      {:else if card.suit === 'diamond'}
        <Diamond size="small" />
      {:else if card.suit === 'club'}
        <Club size="small" />
      {/if}
    </div>
    <div class="card-body">
      {#if card.suit === 'heart'}
        <Heart />
      {:else if card.suit === 'spade'}
        <Spade />
      {:else if card.suit === 'diamond'}
        <Diamond />
      {:else if card.suit === 'club'}
        <Club />
      {/if}
    </div>
  {/if}
</div>

<style>
  .card {
    box-sizing: border-box;
    width: 80px;
    height: 120px;
    border-radius: 4px;
    box-shadow: 0 0 2px rgba(0, 0, 0, 0.5);
    padding: 2px 4px;
    background-color: #fffefe;
  }

  .card:not(.bottom-card) {
    margin-top: -100px;
  }

  .card:not(.top-card) .card-body {
    display: none;
  }

  .card.face-up {
    cursor: pointer;
  }

  .card:not(.face-up) {
    background-color: darkgreen;
  }

  .heart .card-header,
  .diamond .card-header {
    color: #b50303;
  }

  .club .card-header,
  .spade .card-header {
    color: black;
  }

  .card-header {
    box-sizing: border-box;
    height: 18px;
    text-transform: uppercase;
  }

  .card-body {
    box-sizing: border-box;
    height: 59px;
    margin-top: 16px;
    text-align: center;
  }
</style>
