<script lang="ts">
    import { fly, scale } from 'svelte/transition';
    import { expoOut } from 'svelte/easing';
    import { mdiFire, mdiCheck, mdiClose, mdiLoading, mdiMicrophone, mdiMicrophoneOff, mdiCog } from '@mdi/js';
    import MokaApp from '../mokai/components/MokaApp';
    import Alert from '../mokai/components/Alert';
    import Button from '../mokai/components/Button';
    import Icon from '../mokai/components/Icon';
    import Switch from '../mokai/components/Switch';

    let active: boolean = true;
    let progress: string = '80';
</script>

<style>
    main {
        text-align: center;
        padding: 1em;
        max-width: 240px;
        margin: 0 auto;
        background: #A8A8A8;
    }

    @media (min-width: 0px) {
        main {
            max-width: none;
        }
    }
</style>

<MokaApp theme="dark">
    <main>
        <Button class="primary-color white-text" outlined>Footer</Button>
        <input type="range" min="0" max="100" bind:value="{progress}">
        {#if active}
            <div transition:fly="{{ x: 350, duration: 800, easing: expoOut }}">
                <Alert class="green darken-2 green-text text-accent-1" {progress} dense duration="infinite" on:dismiss="{() => { active = false; setTimeout(() => {
                    active = true;
                }, 1500); }}">
                    <div slot="icon">
                        <Icon spin path="{mdiCog}" size="42px"/>
                    </div>
                    <div slot="title">
                        <h3>Reloading</h3>
                    </div>
                    Are you sure ?
                    <div style="display: flex" slot="footer">
                        <Button on:click="{() => active = false}">Accept</Button>
                        <Button on:click="{() => active = false}">Reject</Button>
                    </div>
                </Alert>
            </div>
        {/if}
        <Button on:click="{() => { active = !active }}">
            <div slot="icon">
                <Icon path="{mdiFire}"/>
            </div>
            reset
        </Button>
        <div style="display: flex; align-items: center; justify-content: center;">
            <Switch class="{active ? 'error-color' : 'grey lighten-2'}" bind:checked="{active}" rounded>
                <div slot="on">
                    <Icon class="white-text" path="{mdiCheck}" size="19px"/>
                </div>
                <div slot="off">
                    <Icon class="white-text" path="{mdiClose}" size="19px"/>
                </div>
                <div slot="dot">
                    {#if active}
                        <div in:scale="{{ x: -50, duration: 330, easing: expoOut }}">
                            <Icon class="primary-text" path="{mdiMicrophone}" size="16px"/>
                        </div>
                    {:else}
                        <div in:scale="{{ x: 50, duration: 330, easing: expoOut }}">
                            <Icon class="primary-text" path="{mdiMicrophoneOff}" size="16px"/>
                        </div>
                    {/if}
                </div>
            </Switch>
        </div>
    </main>
</MokaApp>