<script lang="ts">
  import logo from '@/assets/svelte.png'
</script>

<header>
  <img src={logo} alt="logo" />
  <h1>Notes App</h1>
</header>

<style>
  header {
    background-color: #414141;
    display: flex;
    align-items: center;
    padding: 10px;
  }

  img {
    width: 2.5rem;
    margin-right: 10px;
  }

  h1 {
    /* color: #ff3e00; */
    color: #fff;
    text-transform: capitalize;
    font-size: 2rem;
    font-weight: 300;
    line-height: 1;
  }

  @media (min-width: 480px) {
    h1 {
      max-width: none;
    }
  }
</style>
