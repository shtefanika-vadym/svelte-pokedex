<script ✂prettier:content✂="Cg==">
import LayoutHeader from './layout/LayoutHeader/LayoutHeader.svelte'
import LayoutContent from './layout/LayoutContent/LayoutContent.svelte'
import { Router } from 'svelte-navigator'
</script>

<Router primary={false}>
  <main class='layout'>
    <LayoutHeader />
    <div class='layout-content'>
      <LayoutContent />
    </div>

  </main>
</Router>


<style>
  .layout {
  }
  .layout-content {
    padding: 0 100px 100px 100px;
  }
</style>