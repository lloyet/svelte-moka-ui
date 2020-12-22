<script lang="ts">
	let klass = '';
	export { klass as class };
	export let style:string = '';
	export let path:string = undefined;
	export let label:string = undefined;
	export let size:string = '24';
	export let disabled:boolean = false;
</script>

<style lang="scss" src="./Icon.scss"></style>

<i
	aria-label="{label}"
	aria-hidden="true"
	aria-disabled="{disabled}"
	class="m-icon {klass}"
	{style}>
	<svg
		xmlns="http://www.w3.org/2000/svg"
		width="{size}"
		height="{size}"
		viewBox="0 0 24 24">
		<path d="{path}">
			{#if label}
				<title>{label}</title>
			{/if}
		</path>
	</svg>
</i>