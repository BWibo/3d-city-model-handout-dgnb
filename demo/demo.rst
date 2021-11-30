###############################################################################
Demo Fahrplan
###############################################################################

*******************************************************************************
Datendownload
*******************************************************************************

1. UTM-Zone abschätzen

  1. https://www.ldbv.bayern.de/file/png/10317/o/UTM_Zonen.png

2. Mit https://www.koordinaten-umrechner.de eine Kachel auswählen.

  1. Bing Hintergrundkarte wählen
  2. Marienstraße 1, Richrath, Langenfeld
  3. UTM Zone 32, 3571, 5666

3. Goolge: `open nrw citygml lod2`

  1. https://www.google.com/search?channel=nrow5&client=firefox-b-d&q=+open+nrw+citygml+lod2

4. https://www.opengeodata.nrw.de/produkte/geobasis/3dg/lod2_gml/lod2_gml/LoD2_32_357_5666_1_NW.gml


*******************************************************************************
Rohdaten visualisieren
*******************************************************************************

FME Inspector
===============================================================================

1. GUI Allgemein

  1. Feature Liste
  2. Attribute
  3. Tabelle

2D View
-------------------------------------------------------------------------------

1. Hintergrundkarte

3D View
-------------------------------------------------------------------------------

1. Building - BuildingPart zeigen
2. ExternalRef zeigen
3. ThematicSurfaces vs. Building Solid zeigen
4. Geometrietypen zeigen

FZK-Viewer
===============================================================================

1. Element filter
2. Feature filter
3. Properties (Eines Gebäudes)

  1. ExternalReference -> AdV Schlüssel
  2. Verbindung zu ALKIS

4. Flächennormalen
5. Statistics (Query -> Statistics)
6. XML Schema validation
7. MiniAnalyse: (Display -> Colors -> Property Value -> Bldg:StoreysAboveGround)

*******************************************************************************
Analyse mit FME
*******************************************************************************

1. Reader
2. Transformation erklären
3. Coloring erklären
4. Writer erklären


*******************************************************************************
3D Web Visualisierung erstellen
*******************************************************************************

Vorbereitung
===============================================================================

3DcityDB starten
-------------------------------------------------------------------------------

.. code-block:: shell

  cd "/d/dgnb"

  # Cleanup
  rm -rfv gltf/*
  docker rm -f -v citydb
  docker network rm citydb-net
  docker network create citydb-net

  # 3D CityDB
  docker run -d --name citydb \
      -p 5432:5432 \
      --network citydb-net \
      -e POSTGRES_PASSWORD=postgres \
      -e SRID=25832 \
    3dcitydb/3dcitydb-pg:latest-alpine \
      postgres \
      -c max_connections=50 \
      -c shared_buffers=8GB \
      -c effective_cache_size=24GB \
      -c maintenance_work_mem=2GB \
      -c checkpoint_completion_target=0.9 \
      -c wal_buffers=16MB \
      -c default_statistics_target=500 \
      -c random_page_cost=1.1 \
      -c effective_io_concurrency=200 \
      -c work_mem=13981kB \
      -c min_wal_size=4GB \
      -c max_wal_size=16GB \
      -c max_worker_processes=12 \
      -c max_parallel_workers_per_gather=6 \
      -c max_parallel_workers=12 \
      -c max_parallel_maintenance_workers=4

Importer/Exporter
===============================================================================

1. Datenbankverbindung herstellen

Import
-------------------------------------------------------------------------------

1. Pfad Drag&Drop & importieren
2. Datenbankbericht
3. BoundingBox

CityGML Export
-------------------------------------------------------------------------------

Filter erklären
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

1. BBox Filter

  1. BBox aus der DB Sicht kopieren
  2. BBox einfügen, editieren und exportieren

2. SQL Query

  .. code-block:: sql

    SELECT c.id
    FROM cityobject c, building b
    WHERE c.id = b.id
    AND b.storeys_above_ground = 3

3. XML Query

  .. code:: xml

    <query>
      <!-- FeatureType Filter -->

      <typeNames>
        <typeName xmlns:bldg="http://www.opengis.net/citygml/building/2.0">bldg:Building</typeName>
      </typeNames>
      <filter>
        <!-- Logisches UND -->

        <and>
          <!-- Räumlicher Filter -->
          <intersects>
            <valueReference>bldg:boundedBy/bldg:GroundSurface/bldg:lod2MultiSurface</valueReference>
            <polygon srid="4326">
              <exterior>
                6.9553313 51.1324388
                6.9558985 51.1315771
                6.9613020 51.1329915
                6.9626156 51.1315958
                6.9629440 51.1341342
                6.9553313 51.1324388
              </exterior>
            </polygon>
          </intersects>

          <!-- Attribut Filter -->
          <propertyIsLessThan>
            <valueReference>bldg:measuredHeight</valueReference>
            <literal>5</literal>
          </propertyIsLessThan>

        </and>
      </filter>
    </query>

KML/Collada Export
-------------------------------------------------------------------------------

1. Exportieren

  .. code-block:: text

    D:\dgnb\gltf\out.kml

2. KML in GoogleEarth anschauen

CSV-Export
-------------------------------------------------------------------------------

1. Export definieren

  .. code-block:: text

    D:\dgnb\ldbv-attribs.txt

  .. code-block:: text

    Adresse:ADDRESS/STREET ADDRESS/HOUSE_NUMBER
    Gemeindeschluessel:CITYOBJECT_GENERICATTRIB/STRVAL[ATTRNAME='Gemeindeschluessel']
    Stockwerksanzahl:BUILDING/STOREYS_ABOVE_GROUND
    Gebaeudehoehe:BUILDING/MEASURED_HEIGHT
    Datenquelle Bodenhoehe:CITYOBJECT_GENERICATTRIB/STRVAL[ATTRNAME='DatenquelleBodenhoehe']
    Datenquelle Dachhoehe:CITYOBJECT_GENERICATTRIB/STRVAL[ATTRNAME='DatenquelleDachhoehe']
    Datenquelle Lage:CITYOBJECT_GENERICATTRIB/STRVAL[ATTRNAME='DatenquelleLage']
    Aktualitaet Grundriss:CITYOBJECT_GENERICATTRIB/STRVAL[ATTRNAME='Grundrissaktualitaet']

2. CSV exportieren

  .. code-block:: text

    D:\dgnb\attributes.csv

3. CSV anschauen
4. CSV in Google Sheets importieren und sharen

  .. code-block:: text

    https://docs.google.com/spreadsheets/d/1Uy_rn1me1FVaOIkjOZq_RTkOT3_TU-5NUTlxkwyXL-A

3D-WebClient
===============================================================================

1. Webclient starten

  .. code-block:: shell

    cd "/d/dgnb"
    docker rm -f -v webcl
    docker run -dit --name webcl -p 80:8000 \
      -v "$PWD/gltf:/var/www/data/" \
    tumgis/3dcitydb-web-map:v1.9.1

2. Layer hinzufügen
3. Attribute bei Klick zeigen

*******************************************************************************
Docker
*******************************************************************************

3DCityDB Docker starten
===============================================================================

.. code-block:: shell

  cd "/d/dgnb"

  # Cleanup
  docker rm -f -v citydb
  docker network rm citydb-net
  docker network create citydb-net

  # 3D CityDB starten
  docker run -d --name citydb \
      -p 5432:5432 \
      --network citydb-net \
      -e POSTGRES_PASSWORD=postgres \
      -e SRID=25832 \
    3dcitydb/3dcitydb-pg:latest-alpine

Docker Import
===============================================================================

.. code-block:: shell

  docker run -i -t --rm --name impexp \
      --network citydb-net \
      -v "$PWD:/data" \
    3dcitydb/impexp:latest-alpine import \
      -H citydb \
      -d postgres \
      -u postgres \
      -p postgres \
      /data/out.gml

Docker 3DVis Export
===============================================================================

.. code-block:: shell

  rm -r -f gltf/*
  docker run -i -t --rm --name impexp \
      --network citydb-net \
      -v "$PWD:/data" \
    3dcitydb/impexp:latest-alpine export-vis \
      -H citydb \
      -d postgres \
      -u postgres \
      -p postgres \
      -l 2 \
      -D collada \
      -G \
      --gltf-binary \
      --gltf-embed-textures \
      --gltf-draco-compression \
      -O globe \
      -a FMETheme \
      -g auto=250 \
      -j \
      -o /data/gltf/out.kml


Docker Export Table
===============================================================================

.. code-block:: shell

  docker run -i -t --rm --name impexp \
      --network citydb-net \
      -v "$PWD:/data" \
    3dcitydb/impexp:4.3.0-alpine export-table \
      -H citydb \
      -d postgres \
      -u postgres \
      -p postgres \
      -l /data/ldbv-attribs.txt \
      -o /data/attributes.csv
