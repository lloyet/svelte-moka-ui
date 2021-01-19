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
    export let text:boolean = false;
    export let border: string = '';
    export let dismissible: boolean = false;
    export let loading: boolean = false;
    export let progress:string = '0';
    export let active: boolean = false;
    export let style: string = '';
    export let inTrans: any = fly;
    export let outTrans: any = fly;
    export let inOpts: any = { y: -50, duration: 800, easing: quintOut };
    export let outOpts: any = { y: -50, duration: 800, easing: quintOut };
    

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
        class:text
        {style}
        in:inTrans="{inOpts}"
        out:outTrans="{outOpts}">
        <div class="m-alert__wrapper">
            <div class="m-alert__icon">
                <slot name="icon"></slot>
            </div>
            <div class="m-alert__content">
                <slot></slot>
            </div>
            {#if dismissible}
                <div class="m-alert__closer">
                    <button on:click="{clickHandler}">
                        <slot name="close">
                            <Icon path="{mdiClose}"/>
                        </slot>
                    </button>
                </div>
            {/if}
            {#if border}
                <div class="m-alert__border border-{border}"></div>
            {/if}
        </div>
        {#if loading}
            <div class="m-alert__line"></div>
            <div class="m-alert__subline m-alert__dec"></div>
            <div class="m-alert__subline m-alert__inc"></div>
        {:else if progress !== '0'}
            <div class="m-alert__line"></div>
            <div class="m-alert__progress" style="--progress: {progress}%;"></div>
        {/if}
    </div>
{/if}