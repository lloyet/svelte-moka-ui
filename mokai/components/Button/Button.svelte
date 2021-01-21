<script lang="ts">
    import Ripple from '../../actions/Ripple';

    let klass:string = '';
    export { klass as class };
    export let style:string = '';
    export let fab:boolean = false;
    export let icon:boolean = false;
    export let outlined:boolean = false;
    export let rounded: boolean = false;
    export let tile:boolean = false;
    export let flat:boolean  = false;
    export let fixed:boolean = false
    export let text:boolean = false;
    export let block:boolean = false;
    export let bordered:boolean = false;
    export let size: string = 'default';
    export let disabled:boolean = false;
    export let ripple:object = {};
</script>

<style lang="scss" src="./Button.scss"></style>

<button
    class="m-button size-{size} {klass}"
    class:outlined
    class:rounded
    class:bordered
    class:tile
    class:fab
    class:flat
    class:fixed
    class:block
    class:icon
    class:text
    class:disabled
    {style}
    {disabled}
    aria-disabled="{disabled}"
    use:Ripple="{ripple}"
    on:click
    {...$$restProps}>
    <div class="m-button__icon">
        <slot name="icon" />
    </div>
    <div class="m-button__content">
        <slot/>
    </div>
</button>