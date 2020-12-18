<script lang="ts">
	import { scale } from 'svelte/transition';
	import { elasticOut } from 'svelte/easing';
	import Icon from 'mdi-svelte';
	import { mdiFire } from '@mdi/js';
	import Alert from '../components/Alert/Alert.svelte';

	export let name: string;
	let visible: boolean;
</script>

<main>
	<h1>Hello {name}!</h1>
	<Alert bind:visible inTrans="{scale}" inOpts="{{ duration: 1200, easing: elasticOut }}" color="#2ff5a5" rounded dismissible>
		<div slot="icon" style="display: flex; align-items: center; justify-content: center;">
			<Icon path="{mdiFire}"/>
		</div>
		<div style="height: 100%; display: flex; justify-content: center; align-items: center;" slot="content">Visit the <a href="https://svelte.dev/tutorial">Svelte tutooooooooorial</a> to learn how to build</div>
	</Alert>
	<button on:click="{() => { visible = true }}">reset</button>
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
		background: lightgrey;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>