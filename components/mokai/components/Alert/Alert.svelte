<script lang="ts">
	import { createEventDispatcher } from 'svelte';
	import { fly } from 'svelte/transition';
	import { quintOut } from 'svelte/easing';
	import Icon from '../Icon/Icon.svelte';
	import { mdiClose } from '@mdi/js';
	
	const dispatch: ((name: string, detail?: any) => void) = createEventDispatcher();

	let klass = '';
	export { klass as class };
	export let dense: boolean = false;
	export let outlined: boolean = false;
	export let tile: boolean = false;
	export let border: string = 'left';
	export let dismissible: boolean = false;
	export let active: boolean = false;
	export let style: string = '';
	export let inTrans: any = fly;
	export let outTrans: any = fly;
	export let inOpts: any = { x: 200, duration: 800, easing: quintOut };
	export let outOpts: any = { y: 100, duration: 400, easing: quintOut };
	

	const clickHandler = (): void => {
		active = false;
		dispatch('dismiss');
	}
</script>

<style lang="scss" src="./Alert.scss"></style>

{#if active}
	<div
		role="alert"
		class="m-alert {klass} {border.split(' ').map(b => b = `border-${b}`).join(' ')}"
		class:dense
		class:outlined
		class:tile
		{style}
		in:inTrans="{inOpts}"
		out:outTrans="{outOpts}">
		<div class="icon">
			<slot name="icon" />
		</div>
		<div class="content">
			<slot/>
		</div>
		{#if dismissible}
			<div class="closer grey-text text-darken-2">
				<button on:click="{clickHandler}">
					<Icon path="{mdiClose}"/>
				</button>
			</div>
		{/if}
	</div>
{/if}