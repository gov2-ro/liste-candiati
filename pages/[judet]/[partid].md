---
title: Candidați 
hide_title: true
hide_table_of_contents: true
og:
  image: https://raw.githubusercontent.com/gov2-ro/liste-candiati/refs/heads/main/static/assets/lista-candidati.png
---

```sql judete
select distinct Circumscripție	from candidati order by Circumscripție DESC
```

```sql candidati_senat
SELECT  
    "Pozitie lista" as poz, 
    Prenume || ' ' || Nume AS Nume , 
    gen, 
    Partid,
    'https://google.ro?search=' || Nume  || ' ' || Prenume || ' ' || Partid || ' Senat'  AS G, 
    'https://news.google.com/search?q=' || Nume  || ' ' || Prenume || ' ' || Partid || '&hl=ro&gl=RO&ceid=RO:ro' AS gN,
    'https://duckduckgo.com/?q=' || Nume  || ' ' || Prenume || ' ' || Partid || '&kp=-2' AS DDG, 
    'https://www.newsnow.com/ro/?search=' || Nume  || ' ' || Prenume || ' ' || Partid || '&lang=ro' AS NN 
     
    FROM candidati WHERE Circumscripție = '${params.judet}' AND Partid = '${params.partid}' AND  Funcție ='S'  ORDER BY "Pozitie lista" ASC
```

```sql candidati_cd
SELECT  "Pozitie lista" as poz, 
Prenume || ' ' || Nume AS Nume , 
Partid,
gen, 'https://google.ro?search' || Nume AS sGoogleRo 
FROM candidati WHERE Circumscripție = '${params.judet}' AND Partid = '${params.partid}' AND  Funcție ='CD'  ORDER BY "Pozitie lista" ASC
```

```sql partide_judet
select  partid, COUNT(*) as count from candidati  WHERE Circumscripție = '${params.judet}' AND partid NOT NULL GROUP BY partid ORDER BY count DESC 
```

# Candidați {params.partid} {params.judet}

<div class="md:flex gap-6">
    <div class="grow-w-1">        
        <ListaCandidati candidati={candidati_senat} camera="senat" title="Senat" />
    </div>
    <div class="grow-w-1">
        <ListaCandidati candidati={candidati_cd} camera="camera deputaților" title="Camera Deputaților" />
    </div>
 </div>

 ---
Partide:  <ListaPartide judet={params.judet} partide={partide_judet} />

 ----
 
 Alege județul:  <ListaJudete judete={judete} partid={params.partid} />