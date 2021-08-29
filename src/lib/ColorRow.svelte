<script>
    export let background = '#fff';
    export let foreground = '#fff';
    export let name = 'name';
    export let color = '#444444';
    $: rowType = isReadable(color, background) ? 'colorRow' : 'colorRow inverted';

    const open = (event) => {
        let input = event.target.querySelector('input');

        if (input) {
            input.click();
        }
    }

    const getLuminance = (hexColor) => {
        const hex = hexColor.replace('#', '');
        const rgb = parseInt(hex, 16);

        const r = (rgb >> 16) & 0xff;
        const g = (rgb >> 8) & 0xff;
        const b = (rgb >> 0) & 0xff;

        return 0.2126 * r + 0.7152 * g + 0.0722 * b;
    }

    const isReadable = (hexColor, background) => {
        const luminance = getLuminance(hexColor);
        const compare = getLuminance(background);

        const rest = luminance - compare;
        return rest > 40;
    }
</script>

<div on:click={e => open(e)} class="{rowType}" style="--theme-color: {color}; --theme-foreground: {foreground}">
    {name}: {color}
    <input type="color" bind:value={color}>
</div>

<style>
    .colorRow {
        width: 100%;
        font-size: 1.5rem;
        position: relative;
        font-family: Roboto, sans-serif;
        font-weight: bold;
        color: var(--theme-color);
        cursor: pointer;
        padding: 0.5rem;
        text-align: left;
    }

    .colorRow.inverted {
        color: var(--theme-foreground);
        background: var(--theme-color);
    }

    input[type=color] {
        background: none;
        border: 0;
        position: absolute;
        top: 0;
        left: 0;
        height: 100%;
        width: 1rem;
        visibility: hidden;
    }
</style>
