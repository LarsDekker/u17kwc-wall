<script>
  import Counter from "./lib/Counter.svelte";
  import Scores from "./lib/Scores.svelte";
</script>

<main>
  <div class="scores">
    <Scores />
  </div>
  <div class="socials">
    <iframe
      allowfullscreen
      id="wallsio-iframe"
      src="https://my.walls.io/f4gui?nobackground=1&amp;show_header=0"
      style="border:0;height:100%;width:100%"
      loading="lazy"
      title="My social wall"
    />
  </div>
</main>

<style>
  :root {
    font-family: Montserrat, -apple-system, BlinkMacSystemFont, "Segoe UI",
      Roboto, Oxygen, Ubuntu, Cantarell, "Open Sans", "Helvetica Neue",
      sans-serif;
  }

  main {
    text-align: center;
    /* padding: 1em;
    margin: 0 auto; */
    height: 100%;
    display: flex;
  }

  img {
    height: 16rem;
    width: 16rem;
  }

  .socials {
    /* background-color: gray; */
    width: 60%;
  }

  .scores {
    /* position: fixed;
    right: 0; */
    height: 100vh;
    width: 40%;
    padding: 20px;
    /* background-color: green; */
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4rem;
    font-weight: 100;
    line-height: 1.1;
    margin: 2rem auto;
    max-width: 14rem;
  }

  p {
    max-width: 14rem;
    margin: 1rem auto;
    line-height: 1.35;
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
