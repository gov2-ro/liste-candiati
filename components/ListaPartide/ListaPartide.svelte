<script>    

export let judet
export let partide
 

</script>


{#each partide as partid}      

  <a href="/{judet}/{partid.Partid}" class="hover:bg-blue-500 hover:text-white px-1 hover:rounded-mx inline-block ml-1">
    {partid.Partid}</a><small>({partid.count})</small>

{/each}