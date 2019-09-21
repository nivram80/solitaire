<script>
	import Card from "./Card.svelte";
	export let name;
</script>

<style>
	h1 {
		color: black;
	}

	.row {
		display: flex;
		flex-direction: row;
		justify-content: space-around;
		width: 100%;
	}
</style>

<h1>{name}</h1>
<div class="row">
	<Card suit="heart" value="k" />
	<Card suit="spade" value="a" />
	<Card suit="diamond" value="10" />
	<Card suit="club" value="2" />
	<Card suit="heart" value="6" />
	<Card suit="spade" value="j" />
	<Card suit="diamond" value="7" />
</div>
