<script>
    import ColorRow from "./ColorRow.svelte";
    import {onMount} from "svelte";

    export let themeJSON = '';

    let theme = [];
    let background = 'transparent';
    let foreground = 'black';

    onMount(() => {
        if (themeJSON !== '') {
            fetch(themeJSON)
                .then(response => response.json())
                .then((response) => {
                    theme = response.colors
                    background = response.colors[0].color
                    foreground = response.colors[1].color
                })
        }
    });
</script>

<div class="palette" style="--palette-background: {background}; --palette-foreground: {foreground}">
<!--    <p class="palette-title">Colors</p>-->
    <div class="palette-content">
        {#each theme as color}
            <ColorRow background="{background}" foreground="{foreground}" name="{color.name}" color="{color.color}"/>
        {/each}
    </div>
</div>

<style>
    .palette {
        margin: 0;
        background-color: var(--palette-background);
    }

    .palette-content {
        max-width: calc(768px / 1.5);
        padding: 1rem;
        border-right: 2px solid var(--palette-foreground);
    }
</style>
