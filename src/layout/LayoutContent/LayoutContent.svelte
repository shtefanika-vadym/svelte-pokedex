<script>
  import { Route, useNavigate } from 'svelte-navigator'
  import Pokemon from '../../features/Pokemon/Pokemon.svelte'

  const navigate = useNavigate()
</script>

<Route path={'home'}>
  <Pokemon />
</Route>

<Route default>
  {navigate('home')}
</Route>
