<script>
  import Palette from "./lib/Palette.svelte";
  let theme = "theme.json";
</script>

<main>
  <Palette themeJSON="{theme}" />
</main>

<style>
  :root {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen,
      Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
      margin:0;
      padding:0;
  }

  main {
    margin: 0 auto;
  }

  @media (min-width: 480px) {
    h1 {
      max-width: none;
    }

    p {
      max-width: none;
    }
  }
</style>
