.. index:: CityGML Werkzeuge

###############################################################################
Werkzeuge für CityGML
###############################################################################

.. index:: Datenauswahl

*******************************************************************************
Datenauswahl und Übersicht
*******************************************************************************

Vor der Auswahl von Daten lohnt sich ein Blick auf die Übersicht zu den amtlichen
:ref:`Koordinatensystemen <citygml/data-availability:Koordinatensysteme in Deutschland>`
in Deutschland.

Falls die Daten ETRS89 vorliegen, kann man mit dieser Grafik die UTM-Zone der Daten
abschätzen:

.. figure:: https://www.ldbv.bayern.de/file/png/10317/o/UTM_Zonen.png
  :width: 50 %
  :target: https://www.ldbv.bayern.de/file/png/10317/o/UTM_Zonen.png
  :align: center

  Übersicht UTM-Zonen in Deutschland |copy| `LDBV <https://www.ldbv.bayern.de/>`_

https://www.koordinaten-umrechner.de
  Website, auf der sich eine Position in verschiedenen Koordinatensystemen
  anzeigen bzw. Umrechnen lässt. In Deutschland liegen die meisten Daten im
  amtllichen Koordinatensystem ETRS89, UTM-Zone 32N oder 33N vor.

.. index:: 3DCityDB

*******************************************************************************
3D City Database Suite
*******************************************************************************

Sammlung an Open Source Softwarewerkzeugen für den CityGML-Standard.

* `3DCityDB offizielle Homepage <https://www.3dcitydb.org/3dcitydb/>`_
* `3DCityDB Github <https://github.com/3dcitydb>`_
* `3DCityDB Online Dokumentation <https://3dcitydb-docs.readthedocs.io/en/latest/>`_


.. index:: 3DCityDB

3D City Database (3DcityDB)
===============================================================================



.. index:: Visualisierung

*******************************************************************************
Visualisierungswerkzeuge
*******************************************************************************

.. index:: FZKViewer

FZKViewer
===============================================================================

Der FZK-Viewer ist ein Open Source Softwarewerkzeug zur Visualisierung von
standardisierten semantischen Datenmodellen aus den Bereichen
BIM (Building Information Modelling) und GIS (Geographische Informationssysteme),
das vom Karlsruher Institut für Technologie (KIT) entwickelt wird.

* `FZK Viewer Homepage <https://www.iai.kit.edu/1302.php>`_

.. image:: ../img/fzk_viewer.png
  :width: 90 %
  :align: center

.. index:: FME Data Inspector

FME Data Inspector
===============================================================================

Der FME Data Inspector ist das Visualisierungswerkzeug des Safe Software
FME Desktop Softwarepakets. Die Software ist kostenpflichtig und läuft auf
allen gängigen Betriebssystemen. Neben CityGML wird eine große Anzahl weiterer
Format aus dem GIS-Bereich und darüber hinaus unterstützt. Der Viewer ist sowohl
für die Anzeige von 2D, als auch 3D-Daten geeignet.

* `FME Desktop <https://www.safe.com/fme/fme-desktop/>`_
* `FME Desktop Download <https://www.safe.com/support/downloads/>`_

.. image:: ../img/fme-inspector-2d.png
  :width: 90 %
  :align: center

.. image:: ../img/fme-inspector-3d.png
  :width: 90 %
  :align: center

.. index:: Azul

Azul
===============================================================================

Azul ist ein CityGML und CityJSON Viewer, der an der TU-Delft entwickelt wird.
Die Software ist Open Source und unterstützt nur MacOS.

* `Azul Github <https://github.com/tudelft3d/azul>`_

.. image:: ../img/azul.png
  :width: 90 %
  :align: center

.. index:: CityGML Generator

*******************************************************************************
CityGML Generatoren
*******************************************************************************

.. index:: VCS BuildingReconstruction

Virtual City Systems: BuildingReconstruction
===============================================================================

Kommerzielles Werkzeug zur automatisierten Ableitung großer 3D-Stadtmodelle
in LoD1 und LoD2.

* `VCS B-Rec Homepage <https://vc.systems/en/products/building-reconstruction/>`_

.. image:: https://vc.systems/wp-content/uploads/2020/09/brec_attributes_en_web_1920px.png
  :width: 90 %
  :align: center
  :target: https://vc.systems/en/products/building-reconstruction/

.. image:: https://vc.systems/wp-content/uploads/2020/09/brec_roof-library_web_1920px.png
  :width: 90 %
  :align: center
  :target: https://vc.systems/en/products/building-reconstruction/

.. index:: 3dfier

3dfier
===============================================================================

Der 3dfier hebt 2D-Geometrien in die dritte Dimension mit Höhendaten aus
LiDAR-Befliegungen.

* `3dfier Github <https://github.com/tudelft3d/3dfier>`_
* `3dfier Artikel <https://doi.org/10.21105/joss.02866>`_

.. image:: https://github.com/tudelft3d/3dfier/raw/master/docs/images/leiden3dfier.png
  :width: 90 %
  :align: center

.. index:: Datentransformation, Transformation, Analysewerkzeug,
  ETL

*******************************************************************************
Datentransformation und Analysen
*******************************************************************************

.. index:: 3DCityDB

3D City Database (3DCityDB)
===============================================================================

Die 3D City Database ist eines der mächtigsten Analysewerkzeuge für CityGML-Modelle.
Analysen über räumliche und nicht-räumliche Daten sind besonders performant,
da die Serialisierung bzw. De-Serialisierung von XML-Daten während des
Analyseworkflows entfällt und die Indexstrukturen der Datenbank genutzt werden können.
Für komplexe räumliche Abfragen stehen die umfassenden Funktion von
`PostGIS <https://postgis.net>`_ bzw. `Oracle Spatial <https://www.oracle.com/de/
database/spatial/>`_ zur Verfügung.

* :ref:`Links und Referenzen zur 3DCityDB <tools/tools:3D City Database Suite>`

.. index:: FME Workbench

FME Workbench
===============================================================================

.. image:: ../img/fme-workbench.png
  :width: 90 %
  :align: center
s

*******************************************************************************
Weitere Links und Referenzen
*******************************************************************************

`TU Delft CityGML Website <https://nervous-ptolemy-d29bcd.netlify.app/>`_
  Website der TU-Delft 3D-Geoinformation Group Rund um CityGML. Auflistung von
  Tools, Beispieldaten, internationalen CityGML-Datensätzen, uvm.



.. images ---------------------------------------------------------------------
.. |copy| unicode:: U+000A9 .. COPYRIGHT SIGNs