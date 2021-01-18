<script lang="ts">
    import { createEventDispatcher, onMount } from 'svelte';
    import { fly } from 'svelte/transition';
    import { quintOut } from 'svelte/easing';
    import Icon from '../Icon/Icon.svelte';
    import { mdiClose } from '@mdi/js';
    
    const dispatch: ((name: string, detail?: any) => void) = createEventDispatcher();

    let klass = '';
    export { klass as class };
    export let dense: boolean = false;
    export let outlined: boolean = false;
    export let rounded:boolean = false;
    export let tile: boolean = false;
    export let border: string = '';
    export let dismissible: boolean = false;
    export let active: boolean = false;
    export let style: string = '';
    export let inTrans: any = fly;
    export let outTrans: any = fly;
    export let inOpts: any = { x: 150, duration: 800, easing: quintOut };
    export let outOpts: any = { x: 150, duration: 800, easing: quintOut };
    

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
        class:rounded
        {style}
        in:inTrans="{inOpts}"
        out:outTrans="{outOpts}">
        <div class="m-alert__wrapper">
            <div class="m-alert__content">
                <slot />
            </div>
            {#if dismissible}
                <div class="m-alert__closer">
                    <button on:click="{clickHandler}">
                        <Icon path="{mdiClose}"/>
                    </button>
                </div>
            {/if}
            {#if border}
                <div class="m-alert__border border-{border}"></div>
            {/if}
        </div>
    </div>
{/if}