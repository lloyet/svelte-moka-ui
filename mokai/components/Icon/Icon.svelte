<script lang="ts">
    let klass = '';
    export { klass as class };
    export let style:string = '';
    export let path:string = undefined;
    export let label:string = undefined;
    export let rounded:boolean = false;
    export let outlined:boolean = false;
    export let pulse: boolean = false;
    export let spin:boolean = false;
    export let flip:string = '';
    export let tile:boolean = false;
    export let size:string = '22px';
    export let disabled:boolean = false;
</script>

<style lang="scss" src="./Icon.scss"></style>

<i
    aria-label="{label}"
    aria-hidden="true"
    aria-disabled="{disabled}"
    class="m-icon {klass}"
    class:rounded
    class:outlined
    class:tile
    class:pulse
    class:spin
    class:flip-horizontal="{flip.includes('horizontal')}"
    class:flip-vertical="{flip.includes('vertical')}"
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