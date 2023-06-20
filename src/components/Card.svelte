<script lang="ts">
	export let value = '';
	export let suit = '';
	export let color = '';
</script>

<div class="grid-item">
	<div class="top-left">
		{value}<br />
		<div style="color:{color}">{suit}</div>
	</div>
	<div />
	<div />
	<div />
	<div class="heart" style="color:{color}">{suit}</div>
	<div />
	<div />
	<div />
	<div class="bottom-right">
		{value}<br />
		<div style="color:{color};">{suit}</div>
	</div>
</div>

<style>
	.grid-item {
		display: grid;
		background-color: white;
		color: black;
		font-size: 1.5em;
		padding: 10px;
		border-radius: 5%;
		box-shadow: 0px 5px 15px grey;
		width: 180px;
		height: 250px;
		position: absolute;
		top: 20px;
		left: 0;
	}

	.heart {
		text-align: center;
		align-self: center;
		font-size: 2em;
	}

	.top-left {
		padding: 0.1em;
	}

	.bottom-right {
		align-self: end;
		transform: rotate(180deg);
	}
</style>
