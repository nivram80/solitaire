<script>
	import { onMount } from "svelte";
	import Card from "./Card.svelte";

	export let name;

	let shuffledDeck = [];
  const deck = [
    ['A','spade'],
    ['2','spade'],
    ['3','spade'],
    ['4','spade'],
    ['5','spade'],
    ['6','spade'],
    ['7','spade'],
    ['8','spade'],
    ['9','spade'],
    ['10','spade'],
    ['J','spade'],
    ['Q','spade'],
    ['K','spade'],
    ['A','heart'],
    ['2','heart'],
    ['3','heart'],
    ['4','heart'],
    ['5','heart'],
    ['6','heart'],
    ['7','heart'],
    ['8','heart'],
    ['9','heart'],
    ['10','heart'],
    ['J','heart'],
    ['Q','heart'],
    ['K','heart'],
    ['A','diamond'],
    ['2','diamond'],
    ['3','diamond'],
    ['4','diamond'],
    ['5','diamond'],
    ['6','diamond'],
    ['7','diamond'],
    ['8','diamond'],
    ['9','diamond'],
    ['10','diamond'],
    ['J','diamond'],
    ['Q','diamond'],
    ['K','diamond'],
    ['A','club'],
    ['2','club'],
    ['3','club'],
    ['4','club'],
    ['5','club'],
    ['6','club'],
    ['7','club'],
    ['8','club'],
    ['9','club'],
    ['10','club'],
    ['J','club'],
    ['Q','club'],
    ['K','club']
  ];

  onMount(() => {
    shuffledDeck = shuffle(deck);
    console.log(shuffledDeck);
  });

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

<h1>{name}</h1>
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

