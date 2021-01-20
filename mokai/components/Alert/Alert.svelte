<script lang="ts">
    import { createEventDispatcher, onMount } from 'svelte';
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
    export let duration: string = '';
    export let progress:number = 0;
    export let style: string = '';

    const closeHandler = (): void => {
        dispatch('dismiss');
    };

    onMount(() => {
        if (duration !== '' && duration !== 'infinite') {
            progress = 0;
            const period: number = parseInt(duration);
            const coef: number = 100 / period;
            const timer = setInterval(() => {
                if (progress < 100) {
                    progress += coef * 10;
                } else {
                    clearInterval(timer);
                    progress = 0;
                    closeHandler();
                }
            }, 10);
        }
    });
</script>

<style lang="scss" src="./Alert.scss"></style>

<div
    role="alert"
    class="m-alert {klass} {border.split(' ').map(b => b = `border-${b}`).join(' ')}"
    class:dense
    class:outlined
    class:tile
    class:rounded
    class:text
    {style}>
    <div class="m-alert__wrapper">
        <div class="m-alert__icon">
            <slot name="icon"></slot>
        </div>
        <div class="m-alert__content">
            <div class="m-alert__title">
                <slot name="title"></slot>
            </div>
            <div class="m-alert__body">
                <slot></slot>
            </div>
            <div class="m-alert__footer">
                <slot name="footer"></slot>
            </div>
        </div>
        {#if dismissible}
            <div class="m-alert__closer">
                <button on:click="{closeHandler}">
                    <slot name="close">
                        <Icon hover="scale" path="{mdiClose}"/>
                    </slot>
                </button>
            </div>
        {/if}
        {#if border}
            <div class="m-alert__border border-{border}"></div>
        {/if}
    </div>
    {#if duration === 'infinite'}
        <div class="m-alert__line"></div>
        <div class="m-alert__subline m-alert__dec"></div>
        <div class="m-alert__subline m-alert__inc"></div>
    {:else if progress !== '0'}
        <div class="m-alert__line"></div>
        <div class="m-alert__progress" style="--progress: {progress}%;"></div>
    {/if}
</div>