---
title: Listă candidați alegeri parlamentare 2024
hideToc: true
hide_title: true
---


```sql camere
SELECT * FROM (
  VALUES 
('toate', 'Toate'),
('CD', 'Camera deputaților'),
('S', 'Senat')
) AS t(id, label)
```


```sql judete
select  Circumscripție, cod_judet, COUNT(*) AS nr_candidati	from candidati where cod_judet != 'diaspora'  GROUP BY Circumscripție, cod_judet order by Circumscripție ASC
```

```sql partide
-- select distinct Partid || ' – ' || "Nume Partid"   AS partid	from candidati 
select distinct partid	from candidati 
```

```sql candidati_count
SELECT  Partid, count(*) as count FROM candidati where Partid not  null group by Partid order by count DESC  

```
```sql candidati_gen
SELECT  Partid, gen, count(gen) as count FROM candidati where Partid not  null group by Partid, gen order by count DESC 
```
```sql candidati_camera
SELECT  Partid, Funcție as Cameră, count(Funcție) as count FROM candidati where Partid not  null group by Partid, Funcție order by count DESC 
```

```sql count_candidati
select  COUNT(*) as count from candidati  
```

```sql count_candidati_cd
select  COUNT(*) as count from candidati  WHERE  Funcție = 'CD'
```

```sql count_candidati_senat
select  COUNT(*) as count from candidati  WHERE  Funcție = 'S'
```


```sql procent_gen
SELECT 
    gen AS Gender, 
    ROUND(COUNT(*) * 100.0 / (SELECT COUNT(*) FROM candidati)) AS Percentage
FROM candidati
GROUP BY gen;
```

```sql candidati
SELECT  "Pozitie lista" as Poz, 
Prenume || ' ' || Nume AS Nume , 
Partid, Circumscripție as Judet,
gen as Gen, 
Funcție,
'https://google.ro/search?q=' || Nume || ' '  || Prenume  AS Caută
FROM candidati  
WHERE ('${inputs.partid.value}' = 'toate' OR Partid = '${inputs.partid.value}')
AND (Circumscripție = '${inputs.judet.value}' OR  '${inputs.judet.value}' == 'toate') 

AND ('${inputs.camere.value}' = 'toate' OR Funcție = '${inputs.camere.value}')
ORDER BY "Pozitie lista" ASC

```

```sql xpartide
select 'toate' as partid, 9999 as count
union
select partid, count(*) as count from candidati group by partid order by count DESC 

```

```sql xjudete
select 'toate' as judet
union
select distinct Circumscripție as judet	from candidati order by Circumscripție DESC
```

 
```sql partide
select 'toate' as partid, 9999 as count
union
select partid, count(*) as count from candidati group by partid order by count DESC 

```

```sql count_jud 

select   cod_judet, circumscripție as judet, count(*) as count from candidati group by circumscripție, cod_judet

```

<div class="grid grid-flow-row-dense grid-cols-3">
  <div class="col-span-2">
    <AreaMap 
        data={count_jud } 
        areaCol=cod_judet
        geoJsonUrl='/assets/gis/ro.geojson'
        geoId=mnemonic
        value=count
        startingZoom = 6
        link=judet
        height=390
    /> 
  </div>
  <div class="text-2xl  m-2 bg-sky-50">

  <h2 class="bg-sky-200 px-7 py-4">Listă candidați <b>alegeri parlamentare 2024</b></h2>
  



<div class="px-7 py-4 pt-6"> 
   <b>{count_candidati[0].count}</b> candidați, <b>{count_candidati_senat[0].count}</b> pentru Senat și <b>{count_candidati_cd[0].count}</b> pentru Camera Deputaților, dintre care <b>{procent_gen[0].Percentage}%</b> sunt bărbați.
</div>

<div class="text-base	 px-6">Apasă pe hartă sau caută în tabelul de mai jos. </div>

   
  </div>
</div>

 

## Caută candidați  {#if inputs.judet.value != true} în județul **{inputs.judet.value}** {/if}

  <Dropdown 
    data={xjudete} 
    name=judet 
    value=judet 
    title="Județ" 
    defaultValue={['toate']}
/> 



 

<Dropdown 
    data={xpartide} 
    name=partid
    value=Partid
    title="Partid" 
    defaultValue={['toate']}
/> 

<Dropdown
    data={camere} 
    name=camere
    value=id
    title='Camere'
    label=label
    defaultValue={['CD']}	
/>

<DataTable data={candidati} search=true rows=50 >
    <Column id=Poz/> 
    <Column id=Nume/> 
    <Column id=Partid/> 
    <Column id=Judet/> 
    <Column id=Gen/> 
    <Column id=Funcție/> 
    <Column id=Caută contentType=link linkLabel="🔎"/> 
</DataTable>

 

---

## Statistici

<BarChart data={candidati_camera} x="Partid" y="count" series="Cameră"  
colorPalette={[
        'darkred',
        'royalblue'  
        ]}   
echartsOptions={{ xAxis: { axisLabel: {rotate: 45,  interval: 0} , type: "category" }}}
/>
 

 <!-- <BarChart data={candidati_camera} x="Partid" y="count" echartsOptions={{ xAxis: { axisLabel: {rotate: 45,  interval: 0}, type: "category"  }}}/> -->

<BarChart data={candidati_gen} x="Partid" y="count" series="gen"     
type=stacked100   title="Distribuție pe genuri"
colorPalette={[
        'darkred',
        'royalblue'  
        ]}
echartsOptions={{ xAxis: { axisLabel: {rotate: 45,  interval: 0}, type: "category"  }}}
/>


---

 <div class="lista-judete  ">
   <ListaJudete judete={judete} />
 </div>
 

<style>
.lista-judete {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  gap: .2ex;
}
</style>
 
 