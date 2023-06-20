<script lang="ts">
	import { deck, card } from '../stores/deck';
	import Card from './Card.svelte';
	let playedCards = [{ value: '', suit: '', color: '' }];

	let value = '';
	let color = '';
	let suit = '';
	let playedCount = 0;

	const addToArray = () => {
		let x: number = +$deck[$deck.length - 1];
		x++;
		$deck = [...$deck, x + ''];
	};

	const resetDeck = () => {
		$deck = [];
		playedCards = [];
		playedCount = 0;
		$card = '';
		const suits = ['Hearts', 'Diamonds', 'Clubs', 'Spades'];
		const values = ['Ace', 2, 3, 4, 5, 6, 7, 8, 9, 10, 'Jack', 'Queen', 'King'];

		for (let suit in suits) {
			for (let value in values) {
				$deck.push(values[value] + ' of ' + suits[suit]);
			}
		}
	};

	const shuffle = () => {
		let numberOfCards = $deck.length;
		for (let i = 0; i < numberOfCards; i++) {
			let j = Math.floor(Math.random() * numberOfCards);
			let tmp = $deck[i];
			$deck[i] = $deck[j];
			$deck[j] = tmp;
		}
	};

	const deal = () => {
		$card = $deck.pop();
		checkSign($card);
		playedCount++;
	};

	function getSuit(suit: string) {
		let splitted = suit.split(' of ');
		return splitted[1];
	}

	function checkSign(card: string) {
		if ($card[0] === '1') {
			value = '10';
		} else {
			value = $card[0];
		}
		let x = getSuit($card);
		if (x === 'Hearts') {
			suit = '♥';
			color = 'red';
		} else if (x === 'Diamonds') {
			suit = '♦';
			color = 'red';
		} else if (x === 'Spades') {
			suit = '♠';
			color = 'black';
		} else if (x === 'Clubs') {
			suit = '♣';
			color = 'black';
		}
		playedCards[playedCount] = { value, suit, color };
	}

	export { resetDeck, shuffle, deal };
</script>

<div>
	<div class="grid-container">
		{#each playedCards as c}
			<Card value={c.value} suit={c.suit} color={c.color} />
		{/each}
	</div>
</div>

<button on:click={resetDeck}> resetDeck </button>
<button on:click={shuffle}> shuffle </button>
<button on:click={deal}> deal </button>

<style>
	.grid-container {
		position: relative;
		margin-top: 2%;
	}
</style>
