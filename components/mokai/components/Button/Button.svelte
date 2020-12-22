<script lang="ts">
	let klass:string = '';
	export { klass as class };
	export let style:string = '';
	export let outlined:boolean = false;
	export let rounded: boolean = false;
	export let bordered:boolean = false;
	export let disabled:boolean = false;
	export let type:string = 'button';
</script>

<style lang="scss" src="./Button.scss"></style>

<button
	class="m-button {klass}"
	class:outlined
	class:rounded
	class:bordered
	{style}
	{type}
	{disabled}
	aria-disabled="{disabled}"
	on:click
	{...$$restProps}>
	<div class="m-button__icon">
		<slot name="icon" />
	</div>
	<div class="m-button__content">
		<slot/>
	</div>
</button>