<script lang="ts">
    import { scale } from 'svelte/transition';
    import { expoOut } from 'svelte/easing';
    import { mdiFire, mdiClose, mdiCheck } from '@mdi/js';
    import MokaApp from '../mokai/components/MokaApp';
    import Alert from '../mokai/components/Alert';
    import Button from '../mokai/components/Button';
    import Icon from '../mokai/components/Icon';
    import Switch from '../mokai/components/Switch';

    let active: boolean = true;
    let checked:boolean;
</script>

<style>
    main {
        text-align: center;
        padding: 1em;
        max-width: 240px;
        margin: 0 auto;
        background: #A8A8A8;
    }

    @media (min-width: 640px) {
        main {
            max-width: none;
        }
    }

    .alert__content {
        display: flex;
        align-items: center;
        justify-content: center;
    }
</style>

<MokaApp theme="dark">
    <main>
        <Alert class="error-color white-text" border="left" dismissible bind:active on:dismiss="{() => {setTimeout(() => { active = !active }, 1500);}}">
            <div class="alert__content">
                <Icon class="animation-spin" path="{mdiFire}" size="28"/>
                Hello world !
            </div>
        </Alert>
        <Button on:click="{() => { active = !active }}">
            <div slot="icon">
                <Icon path="{mdiFire}"/>
            </div>
            reset
        </Button>
        <div style="display: flex; align-items: center; justify-content: center">
            <Switch class="{checked ? 'error-color' : 'grey lighten-2'}" bind:checked rounded>
                <div slot="on">
                    <Icon class="white-text" path="{mdiCheck}" size="19px"/>
                </div>
                <div slot="off">
                    <Icon class="white-text" path="{mdiClose}" size="19px"/>
                </div>
                <div slot="dot">
                    {#if checked}
                        <div in:scale="{{ x: -50, duration: 330, easing: expoOut }}">😀</div>
                    {:else}
                        <div in:scale="{{ x: 50, duration: 330, easing: expoOut }}">🤯</div>
                    {/if}
                </div>
            </Switch>
        </div>
    </main>
</MokaApp>