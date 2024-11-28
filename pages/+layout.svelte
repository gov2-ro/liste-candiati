<script>
import "@evidence-dev/tailwind/fonts.css";
import "../app.css";
import { EvidenceDefaultLayout } from "@evidence-dev/core-components";
export let data;
</script>

<header class="fixed w-full top-0 z-40 flex h-12 shrink-0 justify-start items-center gap-x-4 border-b border-gray-200 bg-white/90 backdrop-blur print:hidden "><div class="max-w-full mx-auto px-6 sm:px-8 md:px-12 flex flex-1 items-center justify-between" style="max-width: 1800px;"><a href="/" class="block text-sm font-bold text-gray-800">Prezență alegeri</a> <div class="flex gap-2 text-sm items-center"> <div class="flex gap-2 items-center">   </div>  <a class="rounded border-slate-100 bg-violet-600	mr-6 border	 px-2 py-1 shadow" id="obsreg" target="_blank" href="https://votcorect.ro/prezidentiale-parlamentare-2024/observatori/#inregistrare"> 🙏 înregistrează-te ca <b>observator</b> ✨✓</a> &emsp;  <a href="https://votcorect.ro">înapoi la <u>VotCorect</u></a> &rarr;</div></div></header>

<svelte:head>
 	
</svelte:head>

<EvidenceDefaultLayout 
	{data} title="Prezență alegeri"
	homePageName = "Național"
	-logo="/assets/votcorect-alb.svg"
	maxWidth=1800
	hideSidebar=true
	hideTOC
	fullWidth=true
	shideHeader=true
 >
	<slot slot="content" />
</EvidenceDefaultLayout>

 