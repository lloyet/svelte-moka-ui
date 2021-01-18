<script lang="ts">
    export let theme:string = 'light';
</script>

<style type="scss" src="./MokaApp.scss" global></style>

<div class="s-app theme--{theme}">
    <slot />
</div>