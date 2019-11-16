<script>
  import { deck } from './utilities/deck';
  import Pile from './Pile.svelte';
  import Card from './Card.svelte';

  let shuffledDeck = [];
  let stockPile = [];
  let tableau = [];

  const deal = shuffledDeck => {
    let piles = [];

    let firstPileCards = [];
    let secondPileCards = [];
    let thirdPileCards = [];
    let fourthPileCards = [];
    let fifthPileCards = [];
    let sixthPileCards = [];
    let seventhPileCards = [];

    stockPile = shuffledDeck;
    let pileNumber = 1;
    let card = {};
    while (seventhPileCards.length < 7) {
      switch (pileNumber) {
        case 1:
          if (firstPileCards.length < 1) {
            card = stockPile.shift();
            firstPileCards.push(card);
            ++pileNumber;
            card.faceUp = true;
            piles.push({ cards: firstPileCards, pileNumber: 1 });
            break;
          }
        case 2:
          if (secondPileCards.length < 2) {
            card = stockPile.shift();
            secondPileCards.push(card);
            ++pileNumber;
            if (secondPileCards.length === 2) {
              card.faceUp = true;
              piles.push({ cards: secondPileCards, pileNumber: 2 });
            }
            break;
          }
        case 3:
          if (thirdPileCards.length < 3) {
            card = stockPile.shift();
            thirdPileCards.push(card);
            ++pileNumber;
            if (thirdPileCards.length === 3) {
              card.faceUp = true;
              piles.push({ cards: thirdPileCards, pileNumber: 3 });
            }
            break;
          }
        case 4:
          if (fourthPileCards.length < 4) {
            card = stockPile.shift();
            fourthPileCards.push(card);
            ++pileNumber;
            if (fourthPileCards.length === 4) {
              card.faceUp = true;
              piles.push({ cards: fourthPileCards, pileNumber: 4 });
            }
            break;
          }
        case 5:
          if (fifthPileCards.length < 5) {
            card = stockPile.shift();
            fifthPileCards.push(card);
            ++pileNumber;
            if (fifthPileCards.length === 5) {
              card.faceUp = true;
              piles.push({ cards: fifthPileCards, pileNumber: 5 });
            }
            break;
          }
        case 6:
          if (sixthPileCards.length < 6) {
            card = stockPile.shift();
            sixthPileCards.push(card);
            ++pileNumber;
            if (sixthPileCards.length === 6) {
              card.faceUp = true;
              piles.push({ cards: sixthPileCards, pileNumber: 6 });
            }
            break;
          }
        case 7:
          if (seventhPileCards.length < 7) {
            card = stockPile.shift();
            seventhPileCards.push(card);
            pileNumber = 1;
            if (seventhPileCards.length === 7) {
              card.faceUp = true;
              piles.push({ cards: seventhPileCards, pileNumber: 7 });
            }
            break;
          }
      }
    }
    return piles;
  };

  const newDeal = () => {
    shuffledDeck = shuffle(deck);
    tableau = deal(shuffledDeck);
  };

  const onUpdatePile = event => {
    const updatedPile = event.detail;
    tableau = tableau.map(pile => {
      return pile.pileNumber === updatedPile.pileNumber ? updatedPile : pile;
    });
  };

  // Borrowed from https://javascript.info/task/shuffle which is based
  // on https://en.wikipedia.org/wiki/Fisher%E2%80%93Yates_shuffle.
  const shuffle = deck => {
    for (let i = deck.length - 1; i > 0; i--) {
      let j = Math.floor(Math.random() * (i + 1));
      [deck[i], deck[j]] = [deck[j], deck[i]];
    }
    return deck;
  };
</script>

<header class="header">
  <div class="title">
    <h1>Solitaire</h1>
  </div>
  <div class="actions">
    <button on:click={newDeal}>New deal</button>
  </div>
</header>

<main class="main">
  <section class="foundations">
    <div class="foundation diamond-foundation">A</div>
    <div class="foundation heart-foundation">A</div>
    <div class="foundation club-foundation">A</div>
    <div class="foundation spade-foundation">A</div>
  </section>

  <section class="tableau">
    {#each tableau as pile}
      <Pile {pile} on:updatePile={onUpdatePile} />
    {/each}
  </section>
</main>

<style>
  :global(html, body) {
    margin: 0;
    padding: 0;
  }

  .header {
    display: flex;
    flex-direction: row;
    justify-content: flex-start;
    align-items: center;
    width: 100%;
    height: 60px;
    padding: 0 8px;
    background-color: black;
  }

  .title {
    width: 33%;
  }

  .actions {
    -webkit-appearance: none;
    display: flex;
    flex-direction: row;
    justify-content: flex-end;
    width: 66%;
    padding-right: 16px;
  }

  h1 {
    margin: 0;
    padding: 0;
    color: white;
  }

  .main {
    display: grid;
    grid-template-areas: 'foundation tableau';
    grid-template-columns: 100px 1fr;
  }

  :global(button) {
    -webkit-appearance: none;
    width: auto;
    min-width: 100px;
    height: 32px;
    color: white;
    font-size: 13px;
    background-color: rgb(181, 3, 3);
    border: none;
    margin: 0;
    padding: 4px 8px;
    cursor: pointer;
  }

  .foundations {
    grid-area: foundation;
    display: grid;
    flex-direction: column;
    justify-content: center;
    align-items: flex-start;
    padding: 8px 0;
  }

  .foundation {
    margin-bottom: 12px;
    box-sizing: border-box;
    width: 80px;
    height: 120px;
    border-radius: 4px;
    border: 4px solid rgba(0, 0, 0, 0.1);
    padding: 4px 6px;
    font-size: 80px;
    color: rgba(0, 0, 0, 0.1);
    text-align: center;
  }

  .tableau {
    grid-area: tableau;
    display: grid;
    grid-template-columns: repeat(7, 100px);
    padding: 8px 16px;
  }
</style>
