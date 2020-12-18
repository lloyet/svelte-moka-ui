<script lang="ts">
	import { onMount } from 'svelte';
	import { fly } from 'svelte/transition';
	import { quintOut } from 'svelte/easing';
	import Icon from 'mdi-svelte';
	import { mdiClose } from '@mdi/js';
	
	let klass = '';
	export { klass as class };
	export let dense: boolean = false;
	export let outlined: boolean = false;
	export let rounded: boolean = false;
	export let color: string = 'limegreen';
	export let border: string = 'left';
	export let dismissible: boolean = false;
	export let visible: boolean = false;
	export let style: string = '';
	export let inTrans: any = fly;
	export let outTrans: any = fly;
	export let inOpts: any = { x: 100, duration: 800, easing: quintOut };
	export let outOpts: any = { x: 100, duration: 800, easing: quintOut };
	
	const handleShow = (): void => {
		visible = false;
	};
	
	onMount((): void => {
		visible = true;
	});
</script>

<style lang="scss" src="./Alert.scss"></style>

{#if visible}
	<div
	role="alert"
	class="c-alert {klass}"
	class:dense
	class:border
	class:outlined
	style="--padding: {dense ? '5px' : '25px'}; --radius: {rounded ? '5px' : '0'}; --shadow: {outlined ? '0 0 0px 1px #696969' : 'none'}; --color: {color}; border-{border}: 5px solid {color}; {style}"
	in:inTrans="{inOpts}"
	out:outTrans="{outOpts}"
	>
		<div class="icon">
			<slot name="icon" />
		</div>
		<div class="content">
			<slot name="content"/>
		</div>
		{#if dismissible}
			<div class="closer">
				<button class="closer" on:click="{handleShow}">
					<Icon path="{mdiClose}" color="#696969"/>
				</button>
			</div>
		{/if}
	</div>
{/if}