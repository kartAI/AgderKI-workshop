# Geografisk Analyse med AgderKI

Visste du at språkmodeller kan programmere? De er faktisk ganske gode på det også! 
 
I denne workshopen skal vi utforske hvordan gjøre geografiske analyser med Agder KI. Vi skal bruke åpne geografiske datasett - prøve ut ulike teknikker for "prompting", og kjøre analysekoden som AgderKI lager til oss. 

## Teknisk oppsett
AgderKI kan ikke _kjøre_ kode enda. Derfor skal vi kjøre koden i et gratis, midlertidig, miljø fra Google som heter Google Colab. Du må ha en Gmail, eller Google-konto for at det skal fungere. Datasettene vi skal bruke er hentet fra GeoNorge.no, eller fra andre åpne datakilder. 

* Åpne en nettleser med [Google Colab](https://colab.research.google.com/) og logg inn
* Åpne et nytt vindu i nettleseren med [AgderKI](https://agderki.egde.io/)

# Lag et kart av geografiske data

Vi skal varme opp med å få AgderKI til å lage python-kode som viser et interaktivt kart med datasettet vårt. Under er en "prompt" som du kan teste direkte. 

* Kjør prompten i AgderKI
* Kopier koden og legg inn i Google Colab (se screenshot for eksempel)

```

Lag python-kode som viser et interaktivt kart i keplergl. Jeg vil vise byene Lillesand, Grimstad og Kristiansand som punkter i kartet.

Husk å ta med '%pip install' for biblioteker jeg trenger

```

Oppgaver:
1. Få lagd koden med eksempelet over og kjør koden i Colab. (du må legge til kode som Google foreslår underveis)
1. Klarer du lage et kart med andre punkter?
1. Klarer du endre størrelsen

![alt text](chrome_vsSQxIxW1x.gif)

# Befolkningsanalyser

```
Lag python-kode som viser befolkningsdata i datasettet. 
* Bruk KeplerGL.
* Det er feltet 'totalbefolkning' som har befolkningstallet

Datasett: https://adventofgis-data.ams3.digitaloceanspaces.com/Befolkning_42_Agder_4326_BefolkningPaGrunnkretsniva2022.fgb
```

**Oppgave**
1. Lag koden med AgderKI og kjør i Colab
1. Endre fargeskala basert på 'totalbefolkning'
1. Hent ut "config" ved å lage ny kode-blokk og kjør koden: 'map_1.config' 
1. Bruk AgderKI for å utvide koden din til å bruke config-datasettet du fikk ut. 

**Ekstraoppgave**
1. Hent ut kun de kommunene med 10 færrest innbyggere og de med 10 flest innbyggere


# Naturanalyser

Vi skal gjøre natur-analyser basert på datasettet AR50. AR50 inneholder arealtyper for geografiske områder. AR50 har kodelisten for 'artype'.

```
    artype: tekstlig beskrivelse
    10: "Bebygd: Boligfelt, tettsted, by, samferdsel, industriområde o.l.",
    20: "Jordbruk: Fulldyrka jord, overflatedyrka jord og innmarksbeite",
    30: "Skog: Skogdekt areal",
    50: "Snaumark: Fastmark med naturlig vegetasjonsdekke som ikke er skog",
    60: "Myr: Areal som på overflata har preg av myr",
    70: "Bre: Is og snø som ikke smelter i løpet av sommeren",
    81: "Ferskvann: Elv og innsjø",
    82: "Hav",
    99: "Ikke kartlagt"
```

**Datasett**
* Datasettet er: Kommuner (geojson): https://raw.githubusercontent.com/robhop/fylker-og-kommuner/refs/heads/main/Kommuner-L.geojson
* Arealtyper (flatgeobuf): https://adventofgis-data.ams3.digitaloceanspaces.com/ar50_agder.fgb
* Eiendommer (flatgeobuf): https://adventofgis-data.ams3.digitaloceanspaces.com/MatrikkelenEiendomskartTeig_4326_Agder.fgb

**Oppgave**
1. Lag et histogram som viser fordelingen av arealtyper for Agder i antall fotballbaner pr arealtype
1. Hvilken kommune har mest areal med 'Myr' (kode 60)
1. Finn de 5 eiendommene (teigene) i Agder som har flest kvadratmeter myr. Vis resultatet i et KeplerGL-kart. 

**Jukselapp kommuneanalyse**

```
Jeg vil ha oversikt over ulike arealtyper ('artype') i Kristiansand kommune

Datasettet er: Kommuner (geojson): https://raw.githubusercontent.com/robhop/fylker-og-kommuner/refs/heads/main/Kommuner-L.geojson
Arealtyper (flatgeobuf): https://adventofgis-data.ams3.digitaloceanspaces.com/ar50_agder.fgb

Lag python-kode som gjør følgende

1. Velg ut Kommunen "Kristiansand"
1. Gjør en spatial intersect mellom Kristiansand og arealtyper-datasettet
1. Du må konvertere geometrien til UTM33 før du regner ut arealet.
1. Regn ut antall kvadratmeter pr arealtype
1. Regn ut antall norske fotballbaner pr arealtype
1. Lag et histogram som viser antall fotballbaner per arealtype for Kristiansand

Lag tekstlig beskrivelse av artype-kodene med denne kodelisten:
    10: "Bebygd: Boligfelt, tettsted, by, samferdsel, industriområde o.l.",
    20: "Jordbruk: Fulldyrka jord, overflatedyrka jord og innmarksbeite",
    30: "Skog: Skogdekt areal",
    50: "Snaumark: Fastmark med naturlig vegetasjonsdekke som ikke er skog",
    60: "Myr: Areal som på overflata har preg av myr",
    70: "Bre: Is og snø som ikke smelter i løpet av sommeren",
    81: "Ferskvann: Elv og innsjø",
    82: "Hav",
    99: "Ikke kartlagt"

```

**Jukselapp eiendomsanalyse**

```
Jeg vil ha oversikt over ulike hvilke arealtyper ('artype') for eiendommer (teiger). 

Datasettet er: 
Eiendommer (flatgeobuf): https://adventofgis-data.ams3.digitaloceanspaces.com/MatrikkelenEiendomskartTeig_4326_Agder.fgb
Arealtyper (flatgeobuf): https://adventofgis-data.ams3.digitaloceanspaces.com/ar50_agder.fgb

Lag python-kode som gjør følgende

1. Gjør en spatial intersect mellom eiendommer og arealtyper-datasettet
1. Du må konvertere geometrien til UTM33 før du regner ut arealet.
1. Regn ut antall kvadratmeter pr arealtype
1. Regn ut antall norske fotballbaner pr arealtype
1. Finn de eiendommene med høyest kvadratmeter arealtype 60: Myr. Ta med all informasjon/attributter fra de aktuelle Eiendommene

Lag tekstlig beskrivelse av artype-kodene med denne kodelisten:
    10: "Bebygd: Boligfelt, tettsted, by, samferdsel, industriområde o.l.",
    20: "Jordbruk: Fulldyrka jord, overflatedyrka jord og innmarksbeite",
    30: "Skog: Skogdekt areal",
    50: "Snaumark: Fastmark med naturlig vegetasjonsdekke som ikke er skog",
    60: "Myr: Areal som på overflata har preg av myr",
    70: "Bre: Is og snø som ikke smelter i løpet av sommeren",
    81: "Ferskvann: Elv og innsjø",
    82: "Hav",
    99: "Ikke kartlagt"


```


Jukselapp Kilden
```
https://kilden.nibio.no/?topic=arealinformasjon&zoom=9.3&x=6574373.78&y=53644.51&bgLayer=graatone&layers=ar5_arealtype,ar50_arealtype,basis_eiendomsgrenser,basis_gnr_bnr&layers_opacity=0.75,0.75,0.75,0.75&layers_visibility=true,true,true,true

```



