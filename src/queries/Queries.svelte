<script lang="ts">
  import { onMount } from 'svelte'

  import type { UseQueryOptions, UseQueryResult } from '../types'
  import useQueries from './useQueries'

  export let queries: UseQueryOptions[]
  // useful for binding
  export let currentResult: UseQueryResult[]

  let firstRender = true

  onMount(() => {
    firstRender = false
  })

  const queriesStore = useQueries(queries)
  $: currentResult = $queriesStore

  $: {
    if (!firstRender) {
      queriesStore.setQueries(queries)
    }
  }
</script>

<slot name="queries" {currentResult} />
