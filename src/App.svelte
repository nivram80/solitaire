<script>
	import { onMount } from "svelte";
	import { deck } from "./utilities/deck";
	import Card from "./Card.svelte";

	let shuffledDeck = [];
	let stockPile = [];
	let firstPile = [];
	let secondPile = [];
	let thirdPile = [];
	let fourthPile = [];
	let fifthPile = [];
	let sixthPile = [];
	let seventhPile = [];

	const deal = (shuffledDeck) => {
		stockPile = shuffledDeck;
		let pileNumber = 1;
		let card = {};
		while (seventhPile.length < 7) {
			switch (pileNumber) {
				case 1:
					if (firstPile.length < 1) {
						card = stockPile.shift();
						firstPile.push(card);
						++pileNumber;
						break;
					}
				case 2:
					if (secondPile.length < 2) {
						card = stockPile.shift();
						secondPile.push(card);
						++pileNumber;
						break;
					}
				case 3:
					if (thirdPile.length < 3) {
						card = stockPile.shift();
						thirdPile.push(card);
						++pileNumber;
						break;
					}
				case 4:
					if (fourthPile.length < 4) {
						card = stockPile.shift();
						fourthPile.push(card);
						++pileNumber;
						break;
					}
				case 5:
					if (fifthPile.length < 5) {
						card = stockPile.shift();
						fifthPile.push(card);
						++pileNumber;
						break;
					}
				case 6:
					if (sixthPile.length < 6) {
						card = stockPile.shift();
						sixthPile.push(card);
						++pileNumber;
						break;
					}
				case 7:
					if (seventhPile.length < 7) {
						card = stockPile.shift();
						seventhPile.push(card);
						pileNumber = 1;
						break;
					}
			} 
		}
	}
	
	const newDeal = () => {
		shuffledDeck = shuffle(deck);
		// console.log("Shuffled Deck: ", shuffledDeck);

		deal(shuffledDeck);
		console.log("1st Pile: ", firstPile);
		console.log("2nd Pile: ", secondPile);
		console.log("3rd Pile: ", thirdPile);
		console.log("4th Pile: ", fourthPile);
		console.log("5th Pile: ", fifthPile);
		console.log("6th Pile: ", sixthPile);
		console.log("7th Pile: ", seventhPile);
		console.log("Stock Pile: ", stockPile);
	}

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
		grid-template-areas: "foundation tableau";
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
	}

	.tableau {
		grid-area: tableau;
		display: grid;
		grid-template-columns: repeat(7, 1fr);
		padding: 8px 16px;
	}

	.pile {
		width: 120px;
		border: 1px solid black;
	}
</style>

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
		<div class="pile first-pile"></div>
		<div class="pile second-pile"></div>
		<div class="pile third-pile"></div>
		<div class="pile fourth-pile"></div>
		<div class="pile fifth-pile"></div>
		<div class="pile sixth-pile"></div>
		<div class="pile seventh-pile"></div>
		<!-- <Card suit="heart" value="k" />
		<Card suit="spade" value="a" />
		<Card suit="diamond" value="10" />
		<Card suit="club" value="2" />
		<Card suit="heart" value="6" />
		<Card suit="spade" value="j" />
		<Card suit="diamond" value="7" /> -->
	</section>
</main>

