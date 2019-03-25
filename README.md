# OKAPI - Offentlig Kort API

[Kortforsyningen](https://kortforsyningen.dk) har udviklet et modul til indlejring af baggrundskort på hjemmesider. Modulet er tiltænkt webudviklere der har brug for en let implementerbar og fleksibel kortvisning på egen hjemmeside.

Modulet er implementeret i Javascript og er baseret på [OpenLayers 5.3](https://openlayers.org/).

Før brug skal man oprette en bruger på [Kortforsyningen](https://www.kortforsyningen.dk/indhold/min-side-0) og oprette en token.

<p align="center"><img src="doc/eksempel.png" alt="forhåndsvisning" width=75% /></p>

## Sådan gør du

1. Opret en bruger på [Kortforsyningen](https://www.kortforsyningen.dk/indhold/min-side-0)
2. Log ind på kortforsyningen.dk med din nye bruger, og opret en token.
3. Indsæt `<script>`-tag i `<head>`-tagget på din hjemmeside
   - Benyt enten vores CDN: `<script src="https://okapi.kortforsyningen.dk/lib/okapi.min.js"></script>`
   - Eller hav filen liggende på din egen server: `<script src="/path/to/okapi.min.js"></script>`
4. Indsæt `<div id="map" class="geomap" data-token="...">`-tag, dér hvor du vil have kortet.
   - Husk at indsætte din egen token i `data-token`-attributten.

Nu har du et indlejret kort på din hjemmeside.

5. Indsæt `<span class="geomarker">`-tag for hvert punkt, du vil sætte i kortet.

## Indholdsfortegnelse

   * [Installation](#installation)
   * [Anvendelse](#anvendelse)
   * [Kort-parametre](#kort-parametre)
   * [Markør-parametre](#markør-parametre)
   * [Fremsøgning af koordinater](#fremsøgning-af-koordinater)

## Installation

### CDN

```html
<script src="https://okapi.kortforsyningen.dk/lib/okapi.min.js"></script>
```

### Lokal kopi

Download filen: `https://okapi.kortforsyningen.dk/lib/okapi.min.js`

```html
<script src="/path/to/okapi.js"></script>
```

### CSS

Vores standard styling kan findes her: `https://okapi.kortforsyningen.dk/lib/okapi.css`

## Anvendelse

### Simpelt kort

```html
<div
  id="map"
  class="geomap"
  data-token="InsertYourTokenHere">
</div>

<script>
  var map = new okapi.Initialize({});
</script>
```

[Demo](https://okapi.kortforsyningen.dk/examples/simple.html)

### Markører

```html
<span
  class="geomarker"
  data-type="some-type"
  data-title="The marker title"
  data-description="The marker description"
  data-address="The marker address">
</span>

<div
  id="map"
  class="geomap"
  data-type=""
  data-center="auto"
  data-token="InsertYourTokenHere">
</div>

<script>
  var map = new okapi.Initialize({});
</script>
```

[Demo](https://okapi.kortforsyningen.dk/examples/markers-simple.html)


### Flere eksempler

[Alle kort-parametre](https://okapi.kortforsyningen.dk/examples/advanced.html)

[Forskellige markører](https://okapi.kortforsyningen.dk/examples/markers-advanced.html)

[To kort på samme side](https://okapi.kortforsyningen.dk/examples/double.html)

[Andre markør-tooltips](https://okapi.kortforsyningen.dk/examples/tooltip.html)

## Kort-parametre

Følgende parametre kan anvendes i et kort-objekt (class: `geomap`):

#### `data-type`

Angiver hvilke markør-typer, der skal vises på kortet. Hvis man fx har både banker med `data-type="bank"`, og hæveautomater med `data-type="atm"`, kan man vise den ene type med:

`data-type="bank"`

eller begge typer med:

`data-type="atm,bank"`

#### `data-zoom`

Angiv zoomniveau i heltal, for at sætte et specifikt zoom-niveau. Hvis den sættes til `"auto"`, vil kortet selv prøve at finde et passende zoom-niveau, hvor alle markører er med på kortet.
Mulige værdier: 0-13, "auto".

#### `data-center`

Hvis centeret skal automatisk sættes udfra de markører der er på kortet kan denne blive sat til auto: `data-center="auto"`. Hvis denne er sat til `"auto"` behøves `data-center-lat` og `data-center-lon` ikke at blive sat.

#### `data-center-lat` og `data-center-lon`

Angiv centerpunkt for kortet. Et koordinatpar i `WGS84`/`epsg:4326`
Eksempelvis: `data-lat="55.5"` og `data-lon="11.5"`.

Disse er ikke relevante, hvis `data-center` har værdien `auto`.

#### `data-background`

Man kan vælge imellem disse fire forskellige baggrundskort:

- `"dtk_skaermkort"`        (Almindeligt skærmkort)
- `"dtk_skaermkort_daempet"` (Dæmpet skærmkort)
- `"forvaltning"`           (Kort til forvaltning - uden navne)
- `"orto_foraar"`           (ortofoto)

Som standard bliver det dæmpede skærmkort brugt.

#### `data-mylocation`

Angiv om knap til Min Position skal vises.
Mulige værdier: `true` , `false`. Standard = `true`.

#### `data-zoomslider`

Angiv om Zoomslider skal vises.
Mulige værdier: `true` , `false`. Standard = `true`.

#### `data-layerswitcher`

Angiv om funktionen Kortvælger skal vises.
Mulige værdier: `true` , `false`. Standard = `true`.

#### `data-token`

Angiv Kortforsyningen token til autentificering.
Har du ikke allerede en token kan du oprette en [her](https://www.kortforsyningen.dk/indhold/min-side-0 Kortforsyningen).

#### `data-show-popup`

Angiv om der skal vises en popup med mere information når der klikkes på en markør.
Mulige værdier: `true` , `false`. Standard = `true`.

## Markør Parametre

Følgende parametre kan anvendes i et markør-object (class: `geomarker`):

#### `data-type`

Angiver hvilken markør-type det skal være. Det kunne fx være `atm` eller `bank`. Dette kan især være smart hvis man skal vise flere kort på samme side.

#### `data-title`

Angiver titlen på markøren. Kommer frem i popup-boksen.

#### `data-description`

Angiver beskrivelsen eller brødteksten på markøren. Kommer frem i popup-boksen.

#### `data-lat` og `data-lon`

Angiver koordinaterne til markøren. Et koordinatpar i `WGS84`/`epsg:4326`.

```
data-lat="55.674802"
data-lon="12.558091"
```

#### `data-address` 

Angiver adressen hvor markøren skal placeres. Denne behøves ikke at angives hvis lat og lon er angivet. Adressen vil blive slået op i [DAWA-AWS](https://dawa.aws.dk). Det kan f.eks. være `data-address="Roskildevej 32, 2000 Frederiksberg"`.

## Fremsøgning af koordinater

For at finde koordinater til en adresse kan du bruge [OpenStreetMap](https://www.openstreetmap.org) eller [Google Maps](https://maps.google.com). Du kan også bruge API'et til Danmarks AdresseRegister igennem [DAWA-AWS](https://dawa.aws.dk), dette er nok det smarteste valg, hvis man vil lave automatiseret adressesøgning via et API.


### OpenStreetMap

På [OSM](https://www.openstreetmap.org) kan du søge efter din adresse, hvorefter du højreklikker og vælger `Vis adresse`.

Herefter vil koordinaterne fremgå i venstre side af skærmen. Se screendump. Det første tal er breddegrad (lat) og det næste tal er længdegrad (lon).

<p align="center"><img src="doc/osm.png" alt="forhåndsvisning"  /></p>


### Google

På [GoogleMaps](https://maps.google.com) kan du søge efter din adresse, hvorefter du højreklikker og vælger `Hvad er der her?`. Så vil der komme en lille boks op nederst i midten af skærmen. Tryk på tallene i boksen. (se screendump).

<p align="center"><img src="doc/google.1.png" alt="forhåndsvisning"  /></p>

Herefter vil koordinaterne fremgå i venstre side af skærmen. Se screendump. Det første tal er breddegrad (lat) og det næste tal er længdegrad (lon).

<p align="center"><img src="doc/google.2.png" alt="forhåndsvisning"  /></p>


### DAWA-AWS

Her er et eksempel på en adresse, som vi får et koordinat på igennem AWS:

http://dawa.aws.dk/adresser?q=rentemestervej%208,%202400&format=geojson&struktur=mini

Returnerer en samling adresser, hvor koordinaterne står i `geometry.coordinates`:

<p align="center"><img src="doc/dawa.png" alt="forhåndsvisning"  /></p>


### Omregning til decimalgrader

Hvis man ikke har decimalgrader i `WGS84`, kan man transformere dem ved hjælp af Kortforsyningens service: RestGeoKeys. ([Læs mere her](https://kortforsyningen.dk/indhold/geonoegler-rest#koortrans)).

Her er en eksempel-url, man kan sende af sted. Man skal dog indsætte sin egen token først:

https://services.kortforsyningen.dk/?servicename=RestGeokeys_v2&method=koortrans&ingeoref=EPSG:25832&ingeop=550000,6220000&outgeoref=EPSG:4326&token=insertYourToken
