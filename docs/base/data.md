# Data

|                                                                                          |                                                                                                 |
| ---------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------- |
| [agents.csv](http://localhost:5500/old/files/data.html#agents.csv)                       | A simple set of four Agents.                                                                    |
| [amazonia.shp](http://localhost:5500/old/files/data.html#amazonia.shp)                   | Cellular data representing the Amazonia region, in Brazil.                                      |
| [brazilstates.shp](http://localhost:5500/old/files/data.html#brazilstates.shp)           | A shapefile describing the 27 Brazilian states.                                                 |
| [cabecadeboi-neigh.gpm](http://localhost:5500/old/files/data.html#cabecadeboi-neigh.gpm) | Neighborhood files to be used with cabecadeboi database.                                        |
| [cabecadeboi.shp](http://localhost:5500/old/files/data.html#cabecadeboi.shp)             | Topography data from Cabeca de Boi mountain, Minas Gerais, Brazil, with 100x100m of resolution. |
| [cabecadeboi800.shp](http://localhost:5500/old/files/data.html#cabecadeboi800.shp)       | Topography data from Cabeca de Boi mountain, Minas Gerais, Brazil, with 800x800m of resolution. |
| [emas.shp](http://localhost:5500/old/files/data.html#emas.shp)                           | Cellular data representing Emas National Park, Brazil.                                          |
| [gpmlinesDbEmas.gpm](http://localhost:5500/old/files/data.html#gpmlinesDbEmas.gpm)       | Neighborhood files to be used with emas database.                                               |
| [river.shp](http://localhost:5500/old/files/data.html#river.shp)                         | A line describing a river within Emas National Park, in Goias, Brazil.                          |
| [simple.pgm](http://localhost:5500/old/files/data.html#simple.pgm)                       | A simple CellularSpace with one attribute for sugarscape model.                                 |

# Directory

|                                                        |                                                    |
| ------------------------------------------------------ | -------------------------------------------------- |
| [test](http://localhost:5500/old/files/data.html#test) | Directory with files used only for internal tests. |

---

## agents.csv

A simple set of four Agents.

- **File:** [agents.csv](http://localhost:5500/data/agents.csv)
- **Quantity:** 5
- **Separator:** ","
- **Source:** TerraME team

| Attribute  | Type   | Description                            |
| ---------- | ------ | -------------------------------------- |
| age        | number | Age of the agent.                      |
| immune     | string | Whether the agent is immune.           |
| metabolism | number | Energy consumed by time step.          |
| name       | string | Name of the agents.                    |
| vision     | number | Distance in cells the agent can see.   |
| wealth     | number | Amount of sugar the agent starts with. |


---

## amazonia.shp

![](http://localhost:5500/images/amazonia.png)

  
  
Cellular data representing the Amazonia region, in Brazil. It has 50x50km of resolution.

- **Files:** [amazonia.dbf](http://localhost:5500/data/amazonia.dbf), [amazonia.prj](http://localhost:5500/data/amazonia.prj), [amazonia.shp](http://localhost:5500/data/amazonia.shp), [amazonia.shx](http://localhost:5500/data/amazonia.shx)
- **Representation:** polygon
- **Quantity:** 2229
- **Projection:** 'USER:900914', with EPSG: 900914 (PROJ4: '+proj=lcc +lat_0=29.6666666666667 +lon_0=-100.333333333333 +lat_1=31.8833333333333 +lat_2=30.1166666666667 +x_0=2296583.333333 +y_0=9842500 +datum=NAD83 +units=m +no_defs')
- **Source:** This data is a copy of the file with the same name created by terralib package.

| Attribute  | Type   | Description                         |
| ---------- | ------ | ----------------------------------- |
| col        | number | Cell's column.                      |
| distports  | number | Distance to ports.                  |
| distroads  | number | Distance to roads.                  |
| id         | string | Unique identifier (internal value). |
| prodes_10  | number | Percentage of clear-cut area.       |
| prodes_208 | number | Percentage of forest area.          |
| protected  | number | Percentage of indigenous area.      |
| row        | number | Cell's row.                         |

---

## brazilstates.shp

A shapefile describing the 27 Brazilian states.

- **Files:** [brazilstates.dbf](http://localhost:5500/data/brazilstates.dbf), [brazilstates.shp](http://localhost:5500/data/brazilstates.shp), [brazilstates.shx](http://localhost:5500/data/brazilstates.shx)
- **Representation:** polygon
- **Quantity:** 27
- **Projection:** Undefined, with EPSG: 0 (PROJ4: Undefined)
- **Source:** IBGE ([http://www.ibge.gov.br](http://www.ibge.gov.br/))

| Attribute | Type   | Description                  |
| --------- | ------ | ---------------------------- |
| CAPITAL   | string | Name of the state's capital. |
| NOME_UF   | string | Name of the state.           |
| POPUL     | number | Population of the state.     |
| SIGLA     | string | State's initials.            |

---

## cabecadeboi-neigh.gpm

Neighborhood files to be used with cabecadeboi database.

- **File:** [cabecadeboi-neigh.gpm](http://localhost:5500/data/cabecadeboi-neigh.gpm)
- **Connected file/layer:** cabecadeboi900.shp
- **Number of origins:** 121
- **Number of connections:** 1236
- **Source:** TerraME team

---

## cabecadeboi.shp

![](http://localhost:5500/images/cabeca.png)

  
  
Topography data from Cabeca de Boi mountain, Minas Gerais, Brazil, with 100x100m of resolution.

- **Files:** [cabecadeboi.dbf](http://localhost:5500/data/cabecadeboi.dbf), [cabecadeboi.prj](http://localhost:5500/data/cabecadeboi.prj), [cabecadeboi.shp](http://localhost:5500/data/cabecadeboi.shp), [cabecadeboi.shx](http://localhost:5500/data/cabecadeboi.shx)
- **Representation:** polygon
- **Quantity:** 8100
- **Projection:** ['WGS 84 / TM 6 NE', with EPSG: 2311 (PROJ4: '+proj=tmerc +lat_0=0 +lon_0=6 +k=0.9996 +x_0=500000 +y_0=0 +datum=WGS84 +units=m +no_defs')](https://epsg.io/2311)
- **Source:** This data is a copy of the file with the same name created by terralib package.

| Attribute | Type   | Description                                               |
| --------- | ------ | --------------------------------------------------------- |
| col       | number | Cell's column.                                            |
| height    | number | Height of the Cell, measured in values between 0 and 255. |
| id        | string | Unique identifier (internal value).                       |
| row       | number | Cell's row.                                               |

---

## cabecadeboi800.shp

![](http://localhost:5500/images/cabeca2.png)

  
  
Topography data from Cabeca de Boi mountain, Minas Gerais, Brazil, with 800x800m of resolution.

- **Files:** [cabecadeboi800.dbf](http://localhost:5500/data/cabecadeboi800.dbf), [cabecadeboi800.prj](http://localhost:5500/data/cabecadeboi800.prj), [cabecadeboi800.shp](http://localhost:5500/data/cabecadeboi800.shp), [cabecadeboi800.shx](http://localhost:5500/data/cabecadeboi800.shx)
- **Representation:** polygon
- **Quantity:** 144
- **Projection:** ['NAD83', with EPSG: 4269 (PROJ4: '+proj=longlat +datum=NAD83 +no_defs')](https://epsg.io/4269)
- **Source:** This data is a copy of cabecadeboi created by terralib package, using a resolution of 800m.

| Attribute | Type   | Description                                               |
| --------- | ------ | --------------------------------------------------------- |
| col       | number | Cell's column.                                            |
| height    | number | Height of the Cell, measured in values between 0 and 255. |
| id        | string | Unique identifier (internal value).                       |
| row       | number | Cell's row.                                               |

---

## emas.shp

![](http://localhost:5500/images/emas.png)

  
  
Cellular data representing Emas National Park, Brazil. It has 500x500m of resolution.

- **Files:** [emas.dbf](http://localhost:5500/data/emas.dbf), [emas.prj](http://localhost:5500/data/emas.prj), [emas.shp](http://localhost:5500/data/emas.shp), [emas.shx](http://localhost:5500/data/emas.shx)
- **Representation:** polygon
- **Quantity:** 5514
- **Projection:** 'USER:900915', with EPSG: 900915 (PROJ4: '+proj=utm +zone=22 +south +ellps=aust_SA +units=m +no_defs')
- **Source:** This data is a copy of the file with the same name created by terralib package.
- **Reference:** Almeida, Rodolfo M., et al. 'Simulando padroes de incendios no Parque Nacional das Emas, Estado de Goias, Brasil.' X Simposio Brasileiro de Geoinformatica (2008)

| Attribute | Type   | Description                                                                                                               |
| --------- | ------ | ------------------------------------------------------------------------------------------------------------------------- |
| col       | number | Cell's column.                                                                                                            |
| firebreak | number | Cell has a firebreak (1) or not (0).                                                                                      |
| id        | string | Unique identifier (internal value).                                                                                       |
| maxcover  | number | A value between 1 and 5 with the maximum value for the forest cover according to the original data with lower resolution. |
| mincover  | number | A value between 1 and 5 with the minimum value for the forest cover according to the original data with lower resolution. |
| river     | number | Cell has a river (1) or not (0).                                                                                          |
| row       | number | Cell's row.                                                                                                               |

---

## gpmlinesDbEmas.gpm

Neighborhood files to be used with emas database.

- **File:** [gpmlinesDbEmas.gpm](http://localhost:5500/data/gpmlinesDbEmas.gpm)
- **Connected files/layers:** emas.shp and river.shp
- **Number of origins:** 1435
- **Number of connections:** 623
- **Source:** TerraME team

---

## river.shp

A line describing a river within Emas National Park, in Goias, Brazil.

- **Files:** [river.dbf](http://localhost:5500/data/river.dbf), [river.shp](http://localhost:5500/data/river.shp), [river.shx](http://localhost:5500/data/river.shx)
- **Representation:** line
- **Quantity:** 208
- **Projection:** Undefined, with EPSG: 0 (PROJ4: Undefined)
- **Source:** Rodolfo Almeida

---

## simple.pgm

![](http://localhost:5500/images/simple.png)

  
  
A simple CellularSpace with one attribute for sugarscape model.

- **File:** [simple.pgm](http://localhost:5500/data/simple.pgm)
- **Source:** TerraME team

---

## test

Directory with files used only for internal tests. This directory is not available within TerraME installer, but it can be downloaded from GitHub.

- **Files:** 36
- **Extensions:** csv, dbf, gal, gpm, gwt, prj, qix, shp, shx
- **Source:** TerraME team