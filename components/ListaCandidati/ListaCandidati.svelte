<script>
    export let candidati;
    export let camera;
    export let title;
</script>

<div class="xmax-w-md mx-auto mt-10 p-0 pb-3 rounded shadow border">
    <h4 class="bg-sky-100 text-center py-1 font-normal mb-3 font-bold">{title}</h4>
    <div class="my-2"></div>
    {#each candidati as candidat}
    
    <div class="flex  relative leading-none rounded-md px-3 py-1 hover:bg-gray-100 group candidat gen-{candidat.gen}">
        <div class="flex-0">
            <span class="font-bold">{candidat.poz}</span>
            <b class="ml-2 nume">{candidat.Nume}</b>
        </div>
        <div class="relative ml-2 hidden group-hover:block  ">
            <button class="show_options text-gray-500 hover:text-gray-700 focus:outline-none ">
                🔎
            </button>
            <div class="search_options absolute right-0 top-4 bg-white border  z-10 hidden group-hover:flex   items-center space-x-1">
                <a class="p-1 markdown small text-gray-700 hover:shadow-md hover:bg-gray-100 rounded" target="_blank" href="https://google.ro/search?q={candidat.Nume}  {candidat.Partid} {camera}">Google</a>
                <a class="p-1 markdown small text-gray-700 hover:shadow-md hover:bg-gray-100 rounded" target="_blank" href="https://news.google.com/search?q={candidat.Nume}  {candidat.Partid} {camera}&hl=ro&gl=RO&ceid=RO:ro">G_News</a>
                <a class="p-1 markdown small text-gray-700 hover:shadow-md hover:bg-gray-100 rounded" target="_blank" href="https://duckduckgo.com/?q={candidat.Nume}  {candidat.Partid}&kp=-2">DDG</a>
                <a class="p-1 markdown small text-gray-700 hover:shadow-md hover:bg-gray-100 rounded" target="_blank" href="https://www.newsnow.com/ro/?search={candidat.Nume}  {candidat.Partid} &lang=ro">NN</a>
            </div>
        </div>
    </div>
    {/each}
</div>

<style>
.candidat.gen-M .nume {
    background-color: aqua;
}

.candidat.gen-F .nume {
    background-color: lightpink;
}

.candidat.gen-M .nume:after{content: "♂";}
.candidat.gen-F .nume:after{content: "♀";}
/* Ensure search_options persists when hovered */
.group:hover .search_options,
.search_options:hover {
    display: flex;
}

/* Inline links */
.search_options {
    display: none;
    flex-direction: row;
    gap: 8px; /* Adjust spacing between links */
}
</style>
