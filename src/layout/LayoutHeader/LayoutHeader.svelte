<script>
  import { Link } from 'svelte-navigator'
</script>

<header class="parent">
  <Link class="link" to="home">Home</Link>
</header>

<style lang="scss">
  .parent {
    height: 65px;
    padding: 0 29px 0 29px;
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: var(--color-light);
  }
</style>
