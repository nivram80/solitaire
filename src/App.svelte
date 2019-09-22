<script>
	import { onMount } from "svelte";
	import { deck } from "./utilities/deck";
	import Card from "./Card.svelte";

	let shuffledDeck = [];
  
  onMount(() => {
    shuffledDeck = shuffle(deck);
    console.log(shuffledDeck);
  });

	// Borrowed from https://javascript.info/task/shuffle which is based 
	// on https://en.wikipedia.org/wiki/Fisher%E2%80%93Yates_shuffle.
  const shuffle = (deck) => {
    for (let i = deck.length - 1; i > 0; i--) {
      let j = Math.floor(Math.random() * (i + 1));
      [deck[i], deck[j]] = [deck[j], deck[i]];
    }
    return deck;
  }
</script>

<style>
	h1 {
		color: black;
	}

	.main {
		display: grid;
		grid-template-areas: "foundation tableau";
		grid-template-columns: 100px 1fr;
	}

	.foundations {
		grid-area: foundation;
		display: grid;
		flex-direction: column;
		justify-content: center;
		align-items: flex-start;
		padding: 8px 0;
		background-color: black;
	}

	.foundation {
		margin-bottom: 12px;
	}

	.tableau {
		grid-area: tableau;
		display: grid;
		grid-template-columns: repeat(7, 1fr);
		padding: 8px 16px;
	}
</style>

<h1>Solitaire</h1>
<main class="main">
	<section class="foundations">
		<div class="foundation diamond-foundation">
			<Card suit="diamond" value="a" />
		</div>
		<div class="foundation heart-foundation">
			<Card suit="heart" value="a" />		
		</div>
		<div class="foundation club-foundation">
			<Card suit="club" value="a" />
		</div>
		<div class="foundation spade-foundation">
			<Card suit="spade" value="a" />		
		</div>
	</section>

	<section class="tableau">
		<Card suit="heart" value="k" />
		<Card suit="spade" value="a" />
		<Card suit="diamond" value="10" />
		<Card suit="club" value="2" />
		<Card suit="heart" value="6" />
		<Card suit="spade" value="j" />
		<Card suit="diamond" value="7" />
	</section>
</main>

