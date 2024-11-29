---
title: Listă candidați județ, alegeri parlamentare 2024
hide_title: true
og:
  image: https://raw.githubusercontent.com/gov2-ro/liste-candiati/refs/heads/main/static/assets/lista-candidati.png
---

```sql partide_judet
select  Circumscripție as xjudet, partid, COUNT(*) as count from candidati  WHERE Circumscripție = '${params.judet}' AND partid NOT NULL GROUP BY Circumscripție, partid ORDER BY count DESC 
```

```sql count_candidati
select  COUNT(*) as count from candidati  WHERE Circumscripție = '${params.judet}'  
```

```sql count_candidati_cd
select  COUNT(*) as count from candidati  WHERE Circumscripție = '${params.judet}' AND Funcție = 'CD'
```

```sql count_candidati_senat
select  COUNT(*) as count from candidati  WHERE Circumscripție = '${params.judet}' AND Funcție = 'S'
```

```sql candidati_senat
SELECT  
    "Pozitie lista" as poz, 
    Prenume || ' ' || Nume AS Nume , 
    gen, 
    Circumscripție as judet,
    Partid,
    'https://google.ro?search=' || Nume  || ' ' || Prenume || ' ' || Partid || ' Senat'  AS G, 
    'https://news.google.com/search?q=' || Nume  || ' ' || Prenume || ' ' || Partid || '&hl=ro&gl=RO&ceid=RO:ro' AS gN,
    'https://duckduckgo.com/?q=' || Nume  || ' ' || Prenume || ' ' || Partid || '&kp=-2' AS DDG, 
    'https://www.newsnow.com/ro/?search=' || Nume  || ' ' || Prenume || ' ' || Partid || '&lang=ro' AS NN 
     
    FROM candidati WHERE Circumscripție = '${params.judet}'  AND  Funcție ='S'  ORDER BY "Pozitie lista" ASC
```

```sql candidati_cd
SELECT  "Pozitie lista" as poz, 
Prenume || ' ' || Nume AS Nume , gen,
Partid, gen,
Circumscripție as judet,
 'https://google.ro?search=' || Nume  || ' ' || Prenume || ' ' || Partid || ' Senat'  AS G, 
    'https://news.google.com/search?q=' || Nume  || ' ' || Prenume || ' ' || Partid || '&hl=ro&gl=RO&ceid=RO:ro' AS gN,
    'https://duckduckgo.com/?q=' || Nume  || ' ' || Prenume || ' ' || Partid || '&kp=-2' AS DDG, 
    'https://www.newsnow.com/ro/?search=' || Nume  || ' ' || Prenume || ' ' || Partid || '&lang=ro' AS NN 
FROM candidati WHERE Circumscripție = '${params.judet}'  AND  Funcție ='CD'  ORDER BY "Pozitie lista" ASC
```

```sql candidati_x
SELECT  Partid, gen, count(gen) as count FROM candidati WHERE Circumscripție = '${params.judet}' group by Partid, gen

```

# Candidați județul **{params.judet}**
<Alert status="info">
<b>{count_candidati[0].count}</b> candidați, <b>{count_candidati_senat[0].count}</b> pentru Senat și <b>{count_candidati_cd[0].count}</b> pentru Camera Deputaților.
</Alert>


<BarChart data={candidati_x} x="Partid" y="count" echartsOptions={{ xAxis: { axisLabel: {rotate: 75}  }}}
/>
<BarChart data={candidati_x} x="Partid" y="count" series="gen"     
type=stacked100  
echartsOptions={{ xAxis: { axisLabel: {rotate: 75}  }}}
/>


**Alege partid**: <ListaPartide judet={params.judet} partide={partide_judet} />



 {#each partide_judet as partid}      


{#if 1==1}
  ### {partid.Partid}

<div class="md:flex gap-6">
    <div class="grow-w-1">       
        <ListaCandidatiPartid xpartid={partid.Partid} xjudet={params.judet} candidati={candidati_senat} camera="senat" title="Senat" />
    </div>
    <div class="grow-w-1">
        <ListaCandidatiPartid xpartid={partid.Partid} xjudet={params.judet} candidati={candidati_cd} camera="camera deputaților" title="Camera Deputaților" />
    </div>
 </div>

  <a href="/{params.judet}/{partid.Partid}" class="hover:bg-blue-500 hover:text-white px-1 hover:rounded-mx inline-block" >   
  </a>
 {/if}
{/each} 