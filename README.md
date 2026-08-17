# Ruimte voor Water (RvW) Tool

Deze repository bevat een workflow voor het berekenen van de beschikbare ruimte voor water in polders van waterschappen.

## Workflow

De workflow bestaat uit twee hoofdonderdelen:

### 1. Setup script

Het setup notebook bereidt alle invoer voor de berekeningen voor.

Per waterschap wordt een mappenstructuur (zie hieronder) aangemaakt waarin voor iedere polder een aparte map wordt aangemaakt. Vervolgens worden op basis van:

- Poldergrenzen
- Watervlakken
- Peilgegevens
- AHN

een peilgecorrigeerd AHN-raster gegenereerd.

Daarnaast wordt met het landgebruik-script voor iedere polder een landgebruikkaart aangemaakt.

## Mappenstructuur

root_folder/
└── <waterschap>/
    ├── <polder_1>/
    │   ├── _temp_<polder_1>.gdb/
    │   │   ├── sj_<polder_1>
    │   │   ├── water_clipped_<polder_1>
    │   │   └── water_buffer_<x>meter_<polder_1>
    │   ├── <polder_1>.gdb/
    │   │   ├── rekengebied_<polder_1>
    │   │   └── ahn_<polder_1>
    │   ├── peilraster.tif
    │   └── landgebruik.tif
    │
    ├── <polder_2>/
    │   ├── _temp_<polder_2>.gdb/
    │   │   ├── sj_<polder_2>
    │   │   ├── water_clipped_<polder_2>
    │   │   └── water_buffer_<x>meter_<polder_2>
    │   ├── <polder_2>.gdb/
    │   │   ├── rekengebied_<polder_2>
    │   │   └── ahn_<polder_2>
    │   ├── peilraster.tif
    │   └── landgebruik.tif
    │
    └── ...

### 2. RVW_M2 Tool

Het `rvw_m2_tool` notebook gebruikt de resultaten uit de setupfase:

- Peilgecorrigeerd AHN-raster
- Landgebruikkaart

Voor iedere polder wordt vervolgens berekend hoeveel waterberging beschikbaar is per landgebruikscategorie bij een stapsgewijze stijging van het waterpeil (per centimeter).

## Data

De workflow maakt gebruik van verschillende ruimtelijke databronnen:

- **AHN**: hoogtegegevens voor het bepalen van maaiveldhoogtes.
- **Poldergrenzen**: afbakening van de te analyseren polders.
- **Watervlakken**: identificatie van open water binnen de polder.
- **Peilgegevens**: vastgestelde waterpeilen per peilgebied.
- **Landgebruik**: classificatie van het landgebruik voor de analyse van waterberging per landgebruikstype.

Deze datasets worden in het setup-script gecombineerd tot de invoerbestanden voor de `rvw_m2_tool`.
