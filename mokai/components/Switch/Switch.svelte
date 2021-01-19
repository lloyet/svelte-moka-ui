<script lang="ts">
    let klass:string = undefined;
    export { klass as class};
    export let rounded:boolean = undefined;
    export let outlined:boolean = undefined;
    export let checked:boolean = false;
    export let icon:boolean = false;
    export let disabled:boolean = undefined;
</script>

<style lang="scss" src="./Switch.scss"></style>


<label
    class="{klass} m-switch"
    class:rounded
    class:outlined
    class:icon
    class:disabled>
    <input type="checkbox" bind:checked {disabled}>
    <span class="slider">
        <span class="content on">
            <slot name="on"></slot>
        </span>
        <span class="content dot">
            <slot name="dot"></slot>
        </span>
        <span class="content off">
            <slot name="off"></slot>
        </span>
    </span>
</label>