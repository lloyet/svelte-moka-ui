<script lang="ts">
	import { mdiFire } from '@mdi/js';
	import MokaApp from '../components/mokai/components/MokaApp';
	import Alert from '../components/mokai/components/Alert';
	import Button from '../components/mokai/components/Button';
	import Icon from '../components/mokai/components/Icon';

	let active: boolean = true;
</script>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
		background: white;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}

	.alert__content {
		display: flex;
		align-items: center;
		justify-content: center;
	}
</style>

<main>
	<MokaApp theme="dark">
		<Alert class="white-text text-accent-5 primary-color" border="bottom" dismissible bind:active on:dismiss="{() => {setTimeout(() => { active = !active }, 1000);}}">
			<div class="alert__content error-text" slot="icon">
				<Icon path="{mdiFire}" size="32"/>
			</div>
			<div class="grey-text text-darken-3">
				Hello world !
			</div>
		</Alert>
		<Button on:click="{() => { active = !active }}">
			<div slot="icon">
				<Icon path="{mdiFire}"/>
			</div>
			reset
		</Button>
	</MokaApp>
</main>