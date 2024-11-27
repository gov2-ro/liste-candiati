---
title: Caută Candidați
---

```sql candidati
SELECT  "Pozitie lista" as Poz, 
Prenume || ' ' || Nume AS Nume , 
Partid, Circumscripție as Judet,
gen as Gen, 
Funcție,
'https://google.ro/search?q=' || Nume || ' '  || Prenume  AS Caută
FROM candidati  
WHERE ('${inputs.partid.value}' = 'toate' OR Partid = '${inputs.partid.value}')
AND ('${inputs.judet.value}' = 'toate' OR Circumscripție = '${inputs.judet.value}')
ORDER BY "Pozitie lista" ASC

```

```sql partide
select 'toate' as partid, 9999 as count
union
select partid, count(*) as count from candidati group by partid order by count DESC 

```

```sql judete
select 'toate' as judet
union
select distinct Circumscripție as judet	from candidati order by Circumscripție DESC

```
 

<!-- <Dropdown    data={functii}    name=functie    value=id    title='Cameră'    label=label    defaultValue={['CD']}	/> -->

  <Dropdown 
    data={judete} 
    name=judet 
    value=judet 
    title="Județ" 
    defaultValue={['toate']}
/>

 

<Dropdown 
    data={partide} 
    name=partid
    value=Partid
    title="Partid" 
    defaultValue={['toate']}
/> 

<DataTable data={candidati} search=true >
    <Column id=Poz/> 
    <Column id=Nume/> 
    <Column id=Partid/> 
    <Column id=Judet/> 
    <Column id=Gen/> 
    <Column id=Funcție/> 
    <Column id=Caută contentType=link linkLabel="🔎"/> 
</DataTable>