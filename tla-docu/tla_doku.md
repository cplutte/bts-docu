# Dokumentation Thesaurus Linguae Aegyptiae #

**Abstract**
Dieses Dokument beschreibt den Aufbau, die Komponenten und die Funktionsweise des TLA aus technischer Sicht. Dabei werden insbesondere die verschiedenen Komponenten erläutert und die Integration der Eclipse E4 basierten Komponenten aus dem BTS erklärt, sowie deren Voraussetzungen beschrieben.



## Überblick ##

### Verwendete Technologien ###

Folgende Technologien kommen im TLA zum Einsatz.


- Eclipse Virgo, https://eclipse.org/virgo/
- Spring MVC, https://projects.spring.io/spring-framework/
- Eclipse E4 Dependency Injection Framework, https://eclipse.org/e4/
- Eclipse Modeling Framework, EMF, https://www.eclipse.org/modeling/emf/
- EMF Json, http://emfjson.org/
- lightcouch, http://www.lightcouch.org/
- CouchDB, https://couchdb.apache.org/
- Elasticsearch, https://www.elastic.co/
- SiteMesh, http://wiki.sitemesh.org/
- Java Server Pages, JSP, http://www.oracle.com/technetwork/java/javaee/jsp/index.html
- jQuery, https://jquery.com/
- Bootstrap CSS, https://getbootstrap.com/


### Aufbau ###

Der Aufbau des TLA folgt dem MVC-Muster.

![Überblick Aufbau des TLA](file:///C:/IT/TLA_dokumentation/grafiken/overview.png)

Die Überglicksgrafik zeigt die verschiedenen Schichten der Geschäftslogik, der Datenzugriffsschicht und der Anzeigekomponeneten des TLA. Pfeile symbolisieren Abhängigkeiten.

Jede Schicht -- hier als Kästchen symbolisiert -- besteht aus mehreren OSGI-Bundle. Die Bundles werden weiter unten im Einzelnen behandelt.

### Installation ###

Alle Java-OSGi-Komponenten werden in einen Eclipse Virgo-Server installiert. Installationsdetails werden weiter unten ausgeführt. Eclipse Virgo ist basiert auf einem Apache Tomcat-Server mit Erweiterungen zur Unterstützung von OSGi.

Die CouchDB-Instanz sowie die Instanz von Elasticsearch werden separat installiert und laufen unabhängig vom Virgo-Server.

## Backend ##

Das Backend verwendet viele Komponenten der BTS, die als OSGi-Bundles direkt im Eclipe Virgo-Server installiert werden können. Diese müssen nicht extra für den TLA kompilliert werden und bedürfen keiner weiteren Anpassung, da sie bereits so ausgelegt wurden, dass sie in beiden Systemen eingesetzt werden können.

### Übersicht über die Komponenten ###

Überblick über die Komponenten des Backends im Einzelnen.

#### OSGi-Bundles des TLA ####

- `org.bbaw.tla.web`
- `org.fub.tla.web.common`
- `org.fub.tla.web.controller`
- `org.fub.tla.web.controller.impl`

Diese vier Komponenten sind im par-Projekt `org.fub.tla.web.par` zusammengefasst.

#### Gemeinsame Komponenten von BTS und TLA ####

- `org.bbaw.bts.commons.fsaccess_3.1.0`
- `org.bbaw.bts.commons.libs.elasticsearch_3.1.0`
- `org.bbaw.bts.commons_3.1.0`
- `org.bbaw.bts.core.commons.corpus_3.1.0`
- `org.bbaw.bts.core.commons_3.1.0`
- `org.bbaw.bts.core.dao.corpus.couchDB_3.1.0`
- `org.bbaw.bts.core.dao.corpus_3.1.0`
- `org.bbaw.bts.core.dao.couchDB_3.1.0`
- `org.bbaw.bts.core.dao_3.1.0`
- `org.bbaw.bts.core.remote.dao.couchDB_3.1.0`
- `org.bbaw.bts.core.remote.dao_3.1.0`
- `org.bbaw.bts.core.services.corpus.impl_3.1.0`
- `org.bbaw.bts.core.services.corpus_3.1.0`
- `org.bbaw.bts.core.services.impl_3.1.0`
- `org.bbaw.bts.core.services_3.1.0`
- `org.bbaw.bts.db.couchdb_3.1.0`
- `org.bbaw.bts.db_3.1.0`
- `org.bbaw.bts.model.corpus_3.1.0`
- `org.bbaw.bts.model_3.1.0`
- `org.lightcouch_0.6.1`
- `org.eclipselabs.emfjson.couchdb_2.0.0`
- `org.eclipselabs.emfjson_0.6.1`

#### OSGi-Bundles für Eclipse E4 ####

- `org.eclipse.e4.core.commands_0.11.0`
- `org.eclipse.e4.core.contexts.source_1.5.0`
- `org.eclipse.e4.core.contexts_1.5.0`
- `org.eclipse.e4.core.di.annotations.source_1.5.0`
- `org.eclipse.e4.core.di.annotations_1.5.0`
- `org.eclipse.e4.core.di.extensions.source_0.14.0`
- `org.eclipse.e4.core.di.extensions_0.13.0`
- `org.eclipse.e4.core.di.source_1.5.0`
- `org.eclipse.e4.core.di_1.5.0`
- `org.eclipse.e4.core.services.source_2.0.100`
- `org.eclipse.e4.core.services_2.0.100`
- `org.eclipse.e4.emf.xpath_0.1.100`
- `org.eclipse.e4.tools.services_0.12.0`
- `org.eclipse.e4.tools_0.12.0`
- `org.eclipse.e4.ui.di_1.1.0`
- `org.eclipse.e4.ui.progress_0.1.100`
- `org.eclipse.e4.ui.services_1.2.0`
- `org.eclipse.e4.ui.workbench_1.3.0`
- `org.eclipse.emf.common.source_2.12.0`
- `org.eclipse.emf.common_2.12.0`
- `org.eclipse.emf.ecore.change.source_2.11.0`
- `org.eclipse.emf.ecore.change_2.11.0`
- `org.eclipse.emf.ecore.source_2.12.0`
- `org.eclipse.emf.ecore.xmi.source_2.12.0`
- `org.eclipse.emf.ecore.xmi_2.12.0`
- `org.eclipse.emf.ecore_2.13.0`
- `org.eclipse.equinox.concurrent_1.1.0`
- `org.eclipse.equinox.console_1.1.200`

##### Besonders angepasste OSGi-Bundles für Eclipse E4 #####

- `org.fub.tla.emfLibs_1.0.0`
- `org.fub.tla.e4UIModelLib_1.0.0`

### Beschreibung der Komponenten ###

#### `org.bbaw.tla.web` ####

Dieses Bundle enthält das Webfrontend des TLA. Es enthält alle JSP-Seiten, jQuery-Bibliotheken, Image-Resourcen und Spring-Konfigurationen.

##### Ordnerstruktur #####

![Ordnerstruktur: org.bbaw.tla.web](file:///C:/IT/TLA_dokumentation/grafiken/org.bbaw.tla.web-ordner-struktur.bmp)

Die Java-Klassen befinden sich in `src`, `META-INF` enthält die `MANIFEST.MF`, `resources` enthält Resourcen wie Bilder, jQuery-Bibliotheken, CSS-Stylesheets, Fonts etc. die in der Webanwendung eingebunden werden. `WEB-INF` ist das Wurzelverzeichnis der Webanwendungen und enthält die JSPs, SiteMesh-Decorator und Spring-Konfigurationen.

##### Web.xml #####

Die `web.xml` enthält die Konfigurationen für:
- Definition der `root-context.xml`
- Definition des Servlets und der `appServlet/servlet-context.xml`
- Angabe des `ServerOsgiBundleXmlWebApplicationContext` für den OSGi-Kontext, wichtig für Eclipse Virgo und OSGi
- Servlet-Mappings
- SiteMesh-Filterdefinition
- explizite Angabe des UTF-8-Encodings, da es sonst zu Encodingproblemen kam


##### Spring-Konfiguration #####

In der `root-context.xml` werden folgende Beans definiert:
- `org.fub.tla.web.control.StartupListener`, der zur Konfiguration der Webapplikation dient und Werte in den Eclipse E4-Kontext beim Start injiziert; weiter unten wird die Konfiguration genauer erläutert.
- Referenzen auf Controller des TLA, die nicht in diesem OGSi-Bundle enthalten sind, sondern von anderen Bundles zur Verfügung gestellt werden und hier verwenden werten sollen. Bespiele sind: `org.fub.tla.web.controller.TLACorpusController` und `org.fub.tla.web.controller.TLAAdminController`

Die Konfiguration des Servlets ist in `appServlet/servlet-context.xml` abgelegt. Sie enthält:
- Definition des Conversion Services
- des `resources`-Verzeichnises
- den Import for die `controller.xml`-Konfiguration der eigentlichen Controller

Die eigentlichen Spring Controller werden in der `controller.xml`-Datei beschrieben. Sie definiert:
- die Packages für den Packagescan nach annotierten Spring Controllern
- die MVC `controller-view`-Mappings

##### SiteMesh #####

SiteMesh dient dem Zusammenfügen und Rendern der HTML-Seiten aus separat definierten Header, Footer, Menü und Body-Elementen ähnlich wie beispielsweise Apache Tiles. Zur Einbindung genügt die Definition des SiteMesh-Filters in der `web.xml` und die Einbindung der `sitemesh`-Bibliothek in den `classpath`, hier `sitemesh-2.4.2`.

![SiteMesh Überblick](file:///C:/IT/TLA_dokumentation/grafiken/org.bbaw.tla.web-sitemesh.bmp)

Die Definition des SiteMesh-Layouts beginnt in der `decorator.xml`. Diese enthält Definitionen von Dekorierern mit Name, zugehöriger JSP und URL-Pattern. Hier wird auch das Verzeichnis definiert, dass die `decorator` enthält.

Die einzelnen `decorator` werden in JSPs definiert und liegen im `decorator`-Verzeichnis. Eine `decorator`-JSP kann beliebig viele JSPs mittels JSLT-Tags einbinden und so das Seitenlayout definieren, z.B. `<c:import url="/WEB-INF/views/tags/navbar.jsp"/>`.

Im `decorators`-Verzeichnis werden Layouts für die Pfade `/`, `/wl`, `/extras` und `/help` definiert. Die eingebundenen Teilkomponenten wie Menüs, Header, Footer etc. befinden sich im Verzeichnis `/views/tags`. Header, Footer etc. werden ebenfalls als JSPs beschrieben.

![SiteMesh Tags](file:///C:/IT/TLA_dokumentation/grafiken/org.bbaw.tla.web-sitemesh-tags.bmp)

Die einzelnen Views bzw. die Body-Komponenten der einzelnen Ansichten werden im Verzeichnis `/views` bzw. in den jeweiligen Unterverzeichnissen `/views/extras`, `/views/wl` und `/views/help` definiert. 

- `/views` enthält die View-JSPs der Wurzelpfades `/`. Diese sind überwiegend statische Seiten.
- `/views/wl` enthält die Seiten für die Wörterbuch- und Textkorpuspräsentation.
- `/views/extras` enthält die Seiten für den Thesaurus und andere im Hauptmenü unter Extras gruppierte Komponenten
- `/views/help`  enthält Seiten für die Benutzerhilfe und Dokumentation

![SiteMesh Views](file:///C:/IT/TLA_dokumentation/grafiken/org.bbaw.tla.web-sitemesh-views.bmp)

##### `resources`-Verzeichnis #####

Das `resources`-Verzeichnis enthält jQuery-Bibliotheken für bootstrap, jQuery-Components, Datumsformatierung, Dropdown-Menüs, Baumansichten, Anzeige und Formatierung von ägyptischem Text. Ferner CSS-Stylsheets für bootstrap und alle weiteren Komponenten sowie Fonts für fontfaces über die die Akademiefont (`BBAWLibertine_ah.ttf`) ausgeliefert wird. Desweiteren Gyphen und Icons, Bilder etc.

##### Java-Klassen und Spring-Controller #####

![Java-Klassen und Spring-Controller](file:///C:/IT/TLA_dokumentation/grafiken/org.bbaw.tla.web-src.bmp)

Das `org.fub.tla.web.control`-Package enthält die Controller. Das `org.fub.tla.web.internal`-Package enthält den Activator und eine interne Hilfsklasse.
Alle Controller sind Spring-Controller, die über Annoations definiert werden und von Spring verwaltet werden. Diesen werden über Spring per `@Autowired` die TLAController aus dem OSGi-Kontext gegeben.Letztere liegen in den Bundles `org.fub.tla.web.controller` und `org.fub.tla.web.controller.impl`.

###### data-Package ######
Dies enthält Beans für den CustomArgumentResolver, hilfreich für die Formatierung der URL Parameter und das Herausfiltern der Session-Parameter. 
Hier muss man ansonsten nichts weiter bearbeiten.

###### eiditor-Package ######
Enthält den Controller für die TLA-editor-Seiten, für das Laden der TLA-Bearbeiter und damit verbundene Aufgaben.

###### extras-Package ######
Enthält den THS-Controller für die Suche und Anzeige der Thesaurusdaten. Ist auf `/extras*` gemappt.

###### corpus-Package ######
Das `corpus-Package` enthält die bzw. den Controller für Dictionary- und Corpus-Daten unter dem Pfad `/wl/`.


#### `org.fub.tla.web.common` ####

![org.bbaw.tla.web.common](file:///C:/IT/TLA_dokumentation/grafiken/org.bbaw.tla.web.common-overview.bmp)

Das Bundle enthält allgemeine Interfaces und Hilfsklassen des TLA. Es hat keine Abhängigkeiten auf andere Bundles des TLA.
Zu den Interfaces zählen das QueryBean-Interface, das WFGrouopView-Interface.
Zudem enthält das Bundle eine LoggerImpl Implementierung des `org.eclipse.e4.core.services.log.Logger`-E4-Logger-Interfaces. Anpassungen des logging sollten hier vorgenommen werden. Der Logger kann wie im BTS-Bundles injiziert werden. 
Im `StartupController` wird eine Instanz des loggers erzeugt und in den `EclipseContext` gespeichtert. So benutzt die Eclipse-E4-Umgebung diese Instanz der hier definierten Logger-Implementierung.

#### `org.fub.tla.web.controller` ####

![org.fub.tla.web.controller](file:///C:/IT/TLA_dokumentation/grafiken/org.fub.tla.web.controller_overview.bmp)

Das Bundle enthält die Interfaces für die TLA-Controller. TLA-Controller werden von der OSGi-Umgebung erzeugt und zur Verfügung gestellt.

#### `org.fub.tla.web.controller.impl` ####

![org.bbaw.tla.web.controller.imp](file:///C:/IT/TLA_dokumentation/grafiken/org.bbaw.tla.web.controller.impl-overview.bmp)

Das Bundle enthält die Implementierungen für die TLA-Controller. TLA-Controller werden von der OSGi-Umgebung erzeugt und zur Verfügung gestellt.

TLA-Controller bilden die Schnittstelle zwischen den Services der BTS-Bundles, die vom E4 Dependency Injection Framework verwaltet werden, und der Spring/OSGi-Umgebung. TLA-Controller werden von Spring verwaltet, sie werden in der `/spring/module-context.xml` Konfigurationsdatei definiert.

Beispiel für eine OSGi-Bean Definition bestehend aus ID und implementierender Klasse:
 `<bean id="tlaCorpusController" class="org.fub.tla.web.controller.impl.TLACorpusControllerImpl"/>`

Die Beans, TLA-Controller, werden in der `/spring/osgi-context.xml` für die OSGi-Umgebung definiert. Sie werden hier als OSGi-Services definiert. Eine Service Definition besteht aus der Referenz - auf eine Bean-ID - und dem Interface für das der Service in der OSGi-Umgebung veröffentlicht wird.

##### E4 Dependency Injection #####

Die TLA-Controller stellen die Schnittstelle zwischen dem OSGi-basierten Spring DI und dem E4 DI der BTS Komponenten dar. Sie werden über Spring DI erzeugt und über OSGi anderen Bundles zur Verfügung gestellt. Und sie sind zugleich Teil der E4 DI-Umgebung und erhalten BTS OSGi-Services über E4 injiziert. Dazu wird eine `postContstruct`-Methode von der Klasse `TLAAbstractController` geerbt und die `postConstruct`-Methode als allgemeine `default-init-method` in der `module-context.xml` definiert. Diese `postConstruct`-Methode holt sich den EclipseContext und injiziert die Abhängigkeiten auf der akutellen Instanz. Dadurch können in den TLA-Controllern alle Komponenten aus der E4 DI-Umgebung wie in E4 üblich eingebunden und verwendet werden.

### Database: CouchDB ###

Eine CouchDB Instanz wird separat auf dem Server installiert. Die Ports und Authentifikation wird im `StartupController` eingetragen und über die Preference wie in E4 üblich den unteren Diensten zur Verfügung gestellt.

Die CouchDB auf dem Server wird nicht nach außen zugänglich gemacht. Entsprechende Ports werden nach außen von der Firewall des Servers geblockt.

#### Synchronisation der CouchDB ####

Für die Synchronisation der CouchDB des TLA mit der Arbeitsdatenbank CouchDB, die auf aaew64 läuft und der Synchronisation der BTS-Instanzen dient, muss ein Replikationsmechanismus geschrieben werden. Dieser Mechanismus soll:
- nicht automatisch, sondern zu gewählten Zeiten, voraussichtlich ca. zweimal jährlich Daten aus der aaew64-CouchDB in die TLA-CouchDB replizieren
- bei der Replikation sind Filter anzuwenden, um nur zu veröffentliche Dokumente aus der aaew64-CouchDB in die TLA-CouchDB zu replizieren

### Indexer: Elasticsearch ###

geplant:
- separate Elasticsearch Installation, basierend auf Elasticsearch 1.7.3 wegen Abhängigkeiten im BTS und weil höhere Versionen nicht mit Rivern kompatibel sind, das BTS aber River für die Integration von CouchDB und Elasticsearch braucht - die neuen Logstash-Komponenten sind für die Desktopinstallation zu komplex und aufwändig
- Entwicklung eines Indizierungsmechanismus für die Erstellung der Indizees
- wichtig, Indiziees zusammenführen, d.h. nicht wie im BTS jede DB Collection in einen eigenen Index schreiben, sondern alle Corpus-Collections in einen gemeinsamen Index schreiben, um die Suche über mehrere Indizees zu ermöglichen (weil es da Probleme mit der Transportclient-Api von Elasticsearch gibt
- die Indizierung soll auf die Komponenten des TLA/BTS zugreifen können und die Indizeeeinträge anreichern, um effiziente Suche durchführen zu können
- Anreicherungen der Indezeeeinträge sind insb. für die Wörterbucheinträge notwendig, bei denen die verschiedenen Ausprägungen der Schreibungen in Texten, die mit der jeweiligen Lemma-ID lemmatisiert sind, als Liste zu den Wörterbucheinträgen hinzugefügt werden sollen, etc.

### E4 Integration ###

Die Integration von Eclipse E4 in die Eclipse Virgo-Umgebung ist notwendig, um die E4 Dependency Injection für die OSGi-Bundles aus dem BTS nutzen zu können. Daher wird die Eclipse E4 Umgebung im Eclipse Virgo-Server installiert.

Eclipse E4 enthält Abhängigkeiten zu Eclipse EMF, da die E4 Application Modell-Komponenten auf Eclipse EMF basieren. Eclipse EMF kann jedoch nicht ohne Weiteres auf einem Eclipse Virgo-Server installiert werden, da die EMF-Plugins erwarten, in einer Eclipse Desktop-Umgebung zu laufen und Zugriffe auf das lokale Betriebsystem und Dateisystem vornehmen, die in einer Serverumgebung nicht unterstützt werden. Daher kommt es zu Inkompatibilitäten.

Eine Lösung hierzu ist, die Eclipse EMF-Komponenten in eigene Bundles zu wrappen und alle Packages zu exportieren und so anderen Bundles zur Verfügung zu stellen. Sind Eclipse EMF-Komponenten gewrappt, werden die `Activator`-Klassen nicht ansgesprochen und die oben genannten Inkompatibilitäten bleiben aus. Daher wurden alle Eclipse EMF-Komponenten in dem Bundle `org.fub.tla.emfLibs_1.0.0` gewrappt.

Analog zur Problembehandlung der Eclipse EMF-Komponenten wurde mit den Komponenten des E4 UI Modells verfahren. Diese wurden ebenfalls in einem gesonderten Bundle gewrappt und alle Packages exportiert. Das Wrapper Bundle heißt `org.fub.tla.e4UIModelLib_1.0.0`.

##### Lösungsvorschläge aus dem Netz#####

Github Projekt: https://github.com/tarelli/emfwrapper

##### Explizite Registrierung der EMF Models #####

Da durch das wrappen die übliche Registrierungsmechanism von EMF, wie sie in einem Eclipse RCP wie dem BTS funktionieren, durch das Wrappen ausgeschaltet werden, müssen die Models explizit registriert werden. Dies wird im TLA im `StartupListener` in `org.bbaw.tla.web` vorgenommen. Der `StartupListener` wird als Bean registriert und von Spring beim Starten erzeugt.

## Frontend ##

Hier werden verschiedene Komponenten des Frontends beschrieben.

### JSPs ###


### jQuery-Komponenten ###

JQuery Componenten und Bibliotheken

- Bootstrap
- Jqtree
- Select2
- Lolight für tokenizer und syntax highliting; verwedet für egytext.jquery.js
- Egytext.jquery.js – eigene bibliothek für die Präsentation von egytext

### CSS ###
- Popover
- … eigentlich fast alles CSS elemnete


## Datenfluss ##

Hier wird ein Beispiel für den Datenfluss von der Datenbank ins Frontend gegeben.

## Konfiguration ##

Für die Konfiguration wird derzeit hauptsächlich der `StartupController` aus dem `org.bbaw.tla.web`-Bundle verwendet.

Später sollten die Werte der Konfiguration aus einer einfachen Textdatei in den `StartupControler` geladen werden.

## Installation ##

1. Installation der Java Laufzeitumgebung  
2. Installation von Eclipse Virgo
3. Konfiguration des Servers, Ports, Authentifikation
4. Kopiere die im Appendix A aufgelisteten Bundles des TLA, der BTS-Komponenten und deren Abhängigkeiten in das `repository/usr`-Verzeichnis des Eclipse Virgo Servers
5. Installation der CouchDB
6. Konfiguration der CouchDB
7. Installation von Elaticsearch
8. Konfiguration der Elasticsearch
9. Replikation der CouchDB aus der aaew64-CouchDB
10. Indizierung durch Elasticsearch
11. Starten des Eclipse Virgo Servers

## Appendix A ##
 Liste aller OSGi-Bundles im Eclipse Virgo-Server

### Liste der Abhängigkeiten des TLA ###

- `com.google.gson_2.2.4`
- `com.ibm.icu_52.1.1`
- `com.springsource.javax.portlet_2.0.0`
- `com.springsource.javax.portlet_2.0.0`
- `com.springsource.javax.servlet.jsp.jstl_1.2.0`
- `com.springsource.javax.servlet.jsp.jstl_1.2.0`
- `com.springsource.org.aopalliance_1.0.0`
- `com.springsource.org.aopalliance_1.0.0`
- `com.springsource.org.apache.commons.fileupload_1.2.0`
- `com.springsource.org.apache.taglibs.standard_1.1.2`
- `com.springsource.org.aspectj.weaver_1.6.12`
- `guava-18.0`
- `jackson-annotations-2.8.2`
- `jackson-core-2.8.2`
- `javax.ejb_3.1.1`
- `javax.el_2.2.0`
- `javax.inject_1.0.0.v20091030`
- `javax.persistence_2.0.4`
- `javax.servlet.jsp_2.2.0`
- `javax.servlet_3.1.0`
- `javax.validation_1.0.0.GA`
- `javax.xml.rpc_1.1.0`
- `javax.xml_1.3.4`
- `org.apache.commons.codec_1.6.0`
- `org.apache.httpcomponents.httpclient_4.3.6`
- `org.apache.httpcomponents.httpcore_4.3.3`
- `org.apache.lucene.core_3.5.0`
- `org.bbaw.bts.commons.fsaccess_3.1.0`
- `org.bbaw.bts.commons.libs.elasticsearch_3.1.0`
- `org.bbaw.bts.commons_3.1.0`
- `org.bbaw.bts.core.commons.corpus_3.1.0`
- `org.bbaw.bts.core.commons_3.1.0`
- `org.bbaw.bts.core.dao.corpus.couchDB_3.1.0`
- `org.bbaw.bts.core.dao.corpus_3.1.0`
- `org.bbaw.bts.core.dao.couchDB_3.1.0`
- `org.bbaw.bts.core.dao_3.1.0`
- `org.bbaw.bts.core.remote.dao.couchDB_3.1.0`
- `org.bbaw.bts.core.remote.dao_3.1.0`
- `org.bbaw.bts.core.services.corpus.impl_3.1.0`
- `org.bbaw.bts.core.services.corpus_3.1.0`
- `org.bbaw.bts.core.services.impl_3.1.0`
- `org.bbaw.bts.core.services_3.1.0`
- `org.bbaw.bts.db.couchdb_3.1.0`
- `org.bbaw.bts.db_3.1.0`
- `org.bbaw.bts.model.corpus_3.1.0`
- `org.bbaw.bts.model_3.1.0`
- `org.bbaw.tla.web`
- `org.codehaus.jackson.core_1.9.5`
- `org.codehaus.jackson.mapper_1.9.5`
- `org.eclipse.core.commands_3.6.100`
- `org.eclipse.core.contenttype_3.4.200`
- `org.eclipse.core.expressions_3.4.600`
- `org.eclipse.core.jobs_3.6.1`
- `org.eclipse.core.runtime_3.12.0`
- `org.eclipse.e4.core.commands_0.11.0`
- `org.eclipse.e4.core.contexts_1.5.0`
- `org.eclipse.e4.core.di.annotations_1.5.0`
- `org.eclipse.e4.core.di.extensions_0.13.0`
- `org.eclipse.e4.core.di_1.5.0`
- `org.eclipse.e4.core.services_2.0.100`
- `org.eclipse.e4.ui.di_1.1.0`
- `org.eclipse.e4.ui.services_1.2.0`
- `org.eclipse.e4.ui.workbench_1.3.0`
- `org.eclipse.emf.common_2.12.0`
- `org.eclipse.emf.ecore.xmi_2.12.0`
- `org.eclipse.emf.ecore_2.13.0`
- `org.eclipse.equinox.app_1.3.200`
- `org.eclipse.equinox.common_3.8.0`
- `org.eclipse.equinox.ds_1.4.400`
- `org.eclipse.equinox.preferences_3.5.200`
- `org.eclipse.equinox.registry_3.5.400`
- `org.eclipse.equinox.security_1.2.0`
- `org.eclipse.equinox.util_1.0.500`
- `org.eclipse.gemini.blueprint.core_1.0.2`
- `org.eclipse.gemini.blueprint.extender_1.0.2`
- `org.eclipse.gemini.blueprint.io_1.0.2`
- `org.eclipse.osgi.services_3.4.0`
- `org.eclipse.osgi_3.8.2`
- `org.eclipse.virgo.medic_3.6.4`
- `org.eclipse.virgo.web.dm_3.6.4`
- `org.eclipse.virgo.web.servlet.adapter_3.6.4`
- `org.eclipselabs.emfjson.couchdb_2.0.0`
- `org.eclipselabs.emfjson_0.6.1`
- `org.fub.tla.e4UIModelLib_1.0.0`
- `org.fub.tla.emfLibs_1.0.0`
- `org.fub.tla.web.common`
- `org.fub.tla.web.controller.impl`
- `org.fub.tla.web.controller`
- `org.fub.tla.web.par`
- `org.lightcouch_0.6.1`
- `org.slf4j.api_1.7.2`
- `org.slf4j.jcl_1.7.2`
- `org.slf4j.log4j_1.7.2`
- `org.springframework.aop_3.1.0`
- `org.springframework.asm_3.1.0`
- `org.springframework.aspects_3.1.0`
- `org.springframework.beans_3.1.0`
- `org.springframework.context.support_3.1.0`
- `org.springframework.context_3.1.0`
- `org.springframework.core_3.1.0`
- `org.springframework.expression_3.1.0`
- `org.springframework.jdbc_3.1.0`
- `org.springframework.jdbc_3.1.0`
- `org.springframework.jms_3.1.0`
- `org.springframework.orm_3.1.0`
- `org.springframework.oxm_3.1.0`
- `org.springframework.transaction_3.1.0`
- `org.springframework.web.portlet_3.1.0`
- `org.springframework.web.servlet_3.1.0`
- `org.springframework.web_3.1.0`
- `twitter-bootstrap-osgi-2.0.3`




### ext-Verzeichnis ###

- `org.jolokia.osgi_1.0.2.jar`
- `org.osgi.enterprise_4.2.0.v201108120515.jar`
- `org.slf4j.api_1.7.2.v20121108-1250.jar`
- `org.slf4j.jcl_1.7.2.v20121108-1250.jar`
- `org.slf4j.jul_1.7.2.v20121108-1250.jar`
- `org.slf4j.log4j_1.7.2.v20130115-1340.jar`
- `org.slf4j.nop_1.7.2.v201212060727.jar`
- `org.springframework.aop_3.1.0.RELEASE.jar`
- `org.springframework.asm_3.1.0.RELEASE.jar`
- `org.springframework.aspects_3.1.0.RELEASE.jar`
- `org.springframework.beans_3.1.0.RELEASE.jar`
- `org.springframework.context.support_3.1.0.RELEASE.jar`
- `org.springframework.context_3.1.0.RELEASE.jar`
- `org.springframework.core_3.1.0.RELEASE.jar`
- `org.springframework.expression_3.1.0.RELEASE.jar`
- `org.springframework.jdbc_3.1.0.RELEASE.jar`
- `org.springframework.jms_3.1.0.RELEASE.jar`
- `org.springframework.orm_3.1.0.RELEASE.jar`
- `org.springframework.oxm_3.1.0.RELEASE.jar`
- `org.springframework.spring-library_3.1.0.RELEASE.libd`
- `org.springframework.transaction_3.1.0.RELEASE.jar`
- `org.springframework.web.portlet_3.1.0.RELEASE.jar`
- `org.springframework.web.servlet_3.1.0.RELEASE.jar`
- `org.springframework.web_3.1.0.RELEASE.jar`
- `osgi.console.properties`
- `ch.qos.logback.classic_1.0.7.v20121108-1250.jar`
- `ch.qos.logback.core_1.0.7.v20121108-1250.jar`
- `ch.qos.logback.slf4j_1.0.7.v20121108-1250.jar`
- `com.springsource.javax.portlet_2.0.0.v20110525.jar`
- `com.springsource.javax.servlet.jsp.jstl_1.2.0.v20110728.jar`
- `com.springsource.org.aopalliance_1.0.0.jar`
- `com.springsource.org.apache.commons.codec_1.3.0.jar`
- `com.springsource.org.apache.commons.fileupload_1.2.0.v20110525.jar`
- `com.springsource.org.apache.commons.httpclient_3.1.0.jar`
- `com.springsource.org.apache.commons.io_1.4.0.jar`
- `com.springsource.org.apache.taglibs.standard_1.1.2.v20110517.jar`
- `com.springsource.org.aspectj.weaver_1.6.12.RELEASE.jar`
- `javax.annotation_1.1.0.v201108011116.jar`
- `javax.ejb_3.1.1.v201204261316.jar`
- `javax.el_2.2.0.v201108011116.jar`
- `javax.jms_1.1.0.v201205091237.jar`
- `javax.mail_1.4.0.v201005080615.jar`
- `javax.persistence_2.0.4.v201112161009.jar`
- `javax.servlet.jsp_2.2.0.v201112011158.jar`
- `javax.servlet_3.0.0.v201112011016.jar`
- `javax.websocket_1.1.0.v201401130840.jar`
- `javax.xml.rpc_1.1.0.v201005080400.jar`
- `org.apache.catalina.ha_7.0.61.jar`
- `org.apache.catalina.tribes_7.0.61.jar`
- `org.apache.catalina_7.0.61.jar`
- `org.apache.coyote_7.0.61.jar`
- `org.apache.el_7.0.61.jar`
- `org.apache.jasper_7.0.61.jar`
- `org.apache.juli.extras_7.0.61.jar`
- `org.apache.tomcat.api_7.0.61.jar`
- `org.apache.tomcat.util_7.0.61.jar`
- `org.apache.tomcat.websocket_7.0.61.jar`
- `org.eclipse.equinox.cm_1.0.400.v20120319-2029.jar`
- `org.eclipse.equinox.ds_1.4.0.v20120112-1400.jar`
- `org.eclipse.equinox.event_1.2.100.v20111010-1614.jar`
- `org.eclipse.equinox.log_1.2.300.v20120522-2049.jar`
- `org.eclipse.equinox.region_1.1.0.v20120319-1602.jar`
- `org.eclipse.equinox.util_1.0.300.v20111010-1614.jar`
- `org.eclipse.gemini.blueprint.core_1.0.2.RELEASE.jar`
- `org.eclipse.gemini.blueprint.extender_1.0.2.RELEASE.jar`
- `org.eclipse.gemini.blueprint.io_1.0.2.RELEASE.jar`
- `org.eclipse.gemini.management_1.0.5.RELEASE.jar`
- `org.eclipse.gemini.web.core_2.2.7.RELEASE.jar`
- `org.eclipse.gemini.web.tomcat_2.2.7.RELEASE.jar`
- `org.eclipse.jdt.core.compiler.batch_3.10.0.v20140604-1726.jar`
- `org.eclipse.osgi.services_3.3.0.v20120307-2102.jar`
- `org.eclipse.virgo.apps.repository.properties`
- `org.eclipse.virgo.kernel.agent.dm_3.6.4.RELEASE.jar`
- `org.eclipse.virgo.kernel.artifact_3.6.4.RELEASE.jar`
- `org.eclipse.virgo.kernel.deployer.dm_3.6.4.RELEASE.jar`
- `org.eclipse.virgo.kernel.deployer_3.6.4.RELEASE.jar`
- `org.eclipse.virgo.kernel.dmfragment_3.6.4.RELEASE.jar`
- `org.eclipse.virgo.kernel.equinox.extensions_3.6.4.RELEASE.jar`
- `org.eclipse.virgo.kernel.osgi_3.6.4.RELEASE.jar`
- `org.eclipse.virgo.kernel.services_3.6.4.RELEASE.jar`
- `org.eclipse.virgo.kernel.userregion.blueprint.plan`
- `org.eclipse.virgo.kernel.userregion_3.6.4.RELEASE.jar`
- `org.eclipse.virgo.management.fragment_3.6.4.RELEASE.jar`
- `org.eclipse.virgo.management.plan`
- `org.eclipse.virgo.medic.core_3.6.4.RELEASE.jar`
- `org.eclipse.virgo.medic_3.6.4.RELEASE.jar`
- `org.eclipse.virgo.nano.core_3.6.4.RELEASE.jar`
- `org.eclipse.virgo.nano.deployer.api_3.6.4.RELEASE.jar`
- `org.eclipse.virgo.nano.deployer.hot_3.6.4.RELEASE.jar`
- `org.eclipse.virgo.repository_3.6.4.RELEASE.jar`
- `org.eclipse.virgo.util.common_3.6.4.RELEASE.jar`
- `org.eclipse.virgo.util.io_3.6.4.RELEASE.jar`
- `org.eclipse.virgo.util.math_3.6.4.RELEASE.jar`
- `org.eclipse.virgo.util.osgi.manifest_3.6.4.RELEASE.jar`
- `org.eclipse.virgo.util.osgi_3.6.4.RELEASE.jar`
- `org.eclipse.virgo.util.parser.manifest_3.6.4.RELEASE.jar`
- `org.eclipse.virgo.web.core_3.6.4.RELEASE.jar`
- `org.eclipse.virgo.web.dm_3.6.4.RELEASE.jar`
- `org.eclipse.virgo.web.properties`
- `org.eclipse.virgo.web.servlet.adapter_3.6.4.RELEASE.jar`
- `org.eclipse.virgo.web.spring.integration_3.6.4.RELEASE.jar`
- `org.eclipse.virgo.web.tomcat.support_3.6.4.RELEASE.jar`
- `org.eclipse.virgo.web.tomcat_3.6.4.RELEASE.plan`

### usr-Verzeichnis ###

- `org.eclipse.e4.core.commands_0.11.0.201609071804.jar`
- `org.eclipse.e4.core.contexts_1.5.0.v20160504-0909.jar`
- `org.eclipse.e4.core.di.annotations_1.5.0.v20151127-1241.jar`
- `org.eclipse.e4.core.di.extensions_0.13.0.v20150421-2214.jar`
- `org.eclipse.e4.core.di_1.5.0.v20150421-2214.jar`
- `org.eclipse.e4.core.services_2.0.100.v20160509-1032.jar`
- `org.eclipse.e4.ui.di_1.1.0.201609071804.jar`
- `org.eclipse.e4.ui.services_1.2.0.201609071804.jar`
- `org.eclipse.e4.ui.workbench_1.3.0.201609071952.jar`
- `org.eclipse.emf.common_2.12.0.v20160420-0247.jar`
- `org.eclipse.emf.ecore.xmi_2.12.0.v20160420-0247.jar`
- `org.eclipse.emf.ecore_2.13.0.201608261443.jar`
- `org.eclipse.equinox.app_1.3.200.v20130910-1609.jar`
- `org.eclipse.equinox.common_3.8.0.v20160509-1230.jar`
- `org.eclipse.equinox.ds_1.4.400.v20160226-2036.jar`
- `org.eclipse.equinox.preferences_3.5.200.v20140224-1527.jar`
- `org.eclipse.equinox.registry_3.5.400.v20140428-1507.jar`
- `org.eclipse.equinox.security_1.2.0.v20130424-1801.jar`
- `org.eclipse.equinox.util_1.0.500.v20130404-1337.jar`
- `org.eclipse.osgi.services_3.4.0.v20140312-2051.jar`
- `org.eclipse.osgi.util_3.3.100.v20150423-1351.jar`
- `org.eclipselabs.emfjson.couchdb_2.0.0.201610041708.jar`
- `org.eclipselabs.emfjson_0.6.1.201611011510.jar`
- `org.fub.tla.e4UIModelLib_1.0.0.201609071948.jar`
- `org.fub.tla.emfLibs_1.0.0.201609071851.jar`
- `org.lightcouch_0.6.1.jar`
- `org.slf4j.api_1.7.2.v20121108-1250.jar`
- `org.slf4j.jcl_1.7.2.v20121108-1250.jar`
- `org.slf4j.log4j_1.7.2.v20130115-1340.jar`
- `twitter-bootstrap-osgi-2.0.3.jar`
- `com.google.gson_2.2.4.v201311231704.jar`
- `com.ibm.icu_52.1.1.v201501240615.jar`
- `guava-18.0.jar`
- `jackson-annotations-2.8.2.jar`
- `jackson-core-2.8.2.jar`
- `javax.ejb_3.1.1.v201204261316.jar`
- `javax.el_2.2.0.v201108011116.jar`
- `javax.inject_1.0.0.v20091030.jar`
- `javax.persistence_2.0.4.v201112161009.jar`
- `javax.servlet.jsp_2.2.0.v201112011158.jar`
- `javax.servlet_3.1.0.v20140303-1611.jar`
- `javax.validation_1.0.0.GA_v201205091237.jar`
- `javax.xml.rpc_1.1.0.v201005080400.jar`
- `javax.xml_1.3.4.v201005080400.jar`
- `org.apache.commons.codec_1.6.0.v201305230611.jar`
- `org.apache.httpcomponents.httpclient_4.3.6.v201411290715.jar`
- `org.apache.httpcomponents.httpcore_4.3.3.v201411290715.jar`
- `org.apache.lucene.core_3.5.0.v20120725-1805.jar`
- `org.bbaw.bts.commons.fsaccess_3.1.0.201610041627.jar`
- `org.bbaw.bts.commons.libs.elasticsearch_3.1.0.201609301420.jar`
- `org.bbaw.bts.commons_3.1.0.201610181451.jar`
- `org.bbaw.bts.core.commons.corpus_3.1.0.201610181451.jar`
- `org.bbaw.bts.core.commons_3.1.0.201610181507.jar`
- `org.bbaw.bts.core.dao.corpus.couchDB_3.1.0.201611011514.jar`
- `org.bbaw.bts.core.dao.corpus_3.1.0.201611011510.jar`
- `org.bbaw.bts.core.dao.couchDB_3.1.0.201612201215.jar`
- `org.bbaw.bts.core.dao_3.1.0.201612191508.jar`
- `org.bbaw.bts.core.remote.dao.couchDB_3.1.0.201610041627.jar`
- `org.bbaw.bts.core.remote.dao_3.1.0.201610041627.jar`
- `org.bbaw.bts.core.services.corpus.impl_3.1.0.201612191508.jar`
- `org.bbaw.bts.core.services.corpus_3.1.0.201612191508.jar`
- `org.bbaw.bts.core.services.impl_3.1.0.201612191508.jar`
- `org.bbaw.bts.core.services_3.1.0.201612191508.jar`
- `org.bbaw.bts.db.couchdb_3.1.0.201610181451.jar`
- `org.bbaw.bts.db_3.1.0.201610181451.jar`
- `org.bbaw.bts.model.corpus_3.1.0.201610181806.jar`
- `org.bbaw.bts.model_3.1.0.201610181816.jar`
- `org.codehaus.jackson.core_1.9.5.201204111326.jar`
- `org.codehaus.jackson.mapper_1.9.5.201204111326.jar`
- `org.eclipse.core.commands_3.6.100.v20140528-1422.jar`
- `org.eclipse.core.contenttype_3.4.200.v20140207-1251.jar`
- `org.eclipse.core.expressions_3.4.600.v20140128-0851.jar`
- `org.eclipse.core.jobs_3.6.1.v20141014-1248.jar`
- `org.eclipse.core.runtime_3.12.0.v20160606-1342.jar`

### plugin-Verzeichnis ###

- `com.springsource.org.apache.commons.codec_1.3.0.jar`
- `com.springsource.org.apache.commons.httpclient_3.1.0.jar`
- `com.springsource.org.aspectj.weaver_1.6.12.RELEASE.jar`
- `org.apache.felix.gogo.command_0.10.0.v201209301215.jar`
- `org.apache.felix.gogo.runtime_0.10.0.v201209301036.jar`
- `org.apache.felix.gogo.shell_0.10.0.v201211091412.jar`
- `org.apache.mina.core_2.0.2.v201108120515.jar`
- `org.apache.sshd.core_0.5.0.v201108120515.jar`
- `org.eclipse.equinox.cm_1.0.400.v20120319-2029.jar`
- `org.eclipse.equinox.common_3.6.100.v20120509-1351.jar`
- `org.eclipse.equinox.console.ssh_1.0.0.v20120430-1356.jar`
- `org.eclipse.equinox.console_1.0.100.v20121001-124408.jar`
- `org.eclipse.equinox.ds_1.4.0.v20120112-1400.jar`
- `org.eclipse.equinox.event_1.2.100.v20111010-1614.jar`
- `org.eclipse.equinox.region_1.1.0.v20120319-1602.jar`
- `org.eclipse.equinox.simpleconfigurator_1.0.300.v20110815-1744.jar`
- `org.eclipse.equinox.util_1.0.300.v20111010-1614.jar`
- `org.eclipse.gemini.blueprint.core_1.0.2.RELEASE.jar`
- `org.eclipse.gemini.blueprint.extender_1.0.2.RELEASE.jar`
- `org.eclipse.gemini.blueprint.io_1.0.2.RELEASE.jar`
- `org.eclipse.gemini.management_1.0.5.RELEASE.jar`
- `org.eclipse.osgi.services_3.3.0.v20120307-2102.jar`
- `org.eclipse.osgi_3.8.2.v20130124-134944.jar`
- `org.eclipse.virgo.kernel.agent.dm_3.6.4.RELEASE.jar`
- `org.eclipse.virgo.kernel.artifact_3.6.4.RELEASE.jar`
- `org.eclipse.virgo.kernel.deployer_3.6.4.RELEASE.jar`
- `org.eclipse.virgo.kernel.equinox.extensions_3.6.4.RELEASE.jar`
- `org.eclipse.virgo.kernel.kerneldmfragment_3.6.4.RELEASE.jar`
- `org.eclipse.virgo.kernel.model_3.6.4.RELEASE.jar`
- `org.eclipse.virgo.kernel.osgi_3.6.4.RELEASE.jar`
- `org.eclipse.virgo.kernel.services_3.6.4.RELEASE.jar`
- `org.eclipse.virgo.kernel.userregionfactory_3.6.4.RELEASE.jar`
- `org.eclipse.virgo.management.fragment_3.6.4.RELEASE.jar`
- `org.eclipse.virgo.medic.core_3.6.4.RELEASE.jar`
- `org.eclipse.virgo.medic.logbackclassicfragment_3.6.4.RELEASE.jar`
- `org.eclipse.virgo.medic.logbackcorefragment_3.6.4.RELEASE.jar`
- `org.eclipse.virgo.medic_3.6.4.RELEASE.jar`
- `org.eclipse.virgo.nano.core_3.6.4.RELEASE.jar`
- `org.eclipse.virgo.nano.deployer.api_3.6.4.RELEASE.jar`
- `org.eclipse.virgo.nano.deployer.hot_3.6.4.RELEASE.jar`
- `org.eclipse.virgo.nano.management_3.6.4.RELEASE.jar`
- `org.eclipse.virgo.repository_3.6.4.RELEASE.jar`
- `org.eclipse.virgo.util.common_3.6.4.RELEASE.jar`
- `org.eclipse.virgo.util.io_3.6.4.RELEASE.jar`
- `org.eclipse.virgo.util.jmx_3.6.4.RELEASE.jar`
- `org.eclipse.virgo.util.math_3.6.4.RELEASE.jar`
- `org.eclipse.virgo.util.osgi.manifest_3.6.4.RELEASE.jar`
- `org.eclipse.virgo.util.osgi_3.6.4.RELEASE.jar`
- `org.eclipse.virgo.util.parser.launcher_3.6.4.RELEASE.jar`
- `org.eclipse.virgo.util.parser.manifest_3.6.4.RELEASE.jar`
- `org.slf4j.api_1.7.2.v20121108-1250.jar`
- `org.slf4j.jcl_1.7.2.v20121108-1250.jar`
- `org.slf4j.jul_1.7.2.v20121108-1250.jar`
- `org.springframework.aop_3.1.0.RELEASE.jar`
- `org.springframework.asm_3.1.0.RELEASE.jar`
- `org.springframework.beans_3.1.0.RELEASE.jar`
- `org.springframework.context_3.1.0.RELEASE.jar`
- `org.springframework.core_3.1.0.RELEASE.jar`
- `org.springframework.expression_3.1.0.RELEASE.jar`
- `osgi.enterprise_4.2.0.v201108120515.jar`
- `ch.qos.logback.classic_1.0.7.v20121108-1250.jar`
- `org.eclipse.virgo.kernel.userregion_3.6.4.RELEASE.jar`
- `org.eclipse.virgo.shell.command_3.6.4.RELEASE.jar`
- `ch.qos.logback.core_1.0.7.v20121108-1250.jar`
- `ch.qos.logback.slf4j_1.0.7.v20121108-1250.jar`
- `com.springsource.org.aopalliance_1.0.0.jar`