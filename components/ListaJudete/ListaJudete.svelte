<script>
export let judete
export let partid

if (partid === undefined) {
  partid = ''
}

</script>

{#each judete as judet}      

  <a href="/{judet.Circumscripție}/{partid}" class="hover:bg-blue-500 hover:text-white px-1 hover:rounded-mx inline-block">
    <b>{judet.Circumscripție} </b> 
    {#if judet.nr_candidati}
    <small>({judet.nr_candidati} )</small>
    {/if}
  </a>

{/each}