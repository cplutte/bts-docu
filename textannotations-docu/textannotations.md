# Text Annotation Erweiterung #

## Übersicht ##

Die Text Annotation Erweiterung ist eine Erweiterung des Berlin Text Systems (BTS) und unterstützt die Erstellung und Bearbeitung von Textannotationen und insbesondere die Anzeige und von überlappenden und mehrschichtigen Annotationen. Vordefinierte Formulare für verschiedene Annotationstypen mit vordefinierten Wertelisten und Auswahlmenüs erlauben die einfache und standardisierte Eingabe von Annotationen. Farbliche Kennzeichnung und Anzeige von Annotationsinhalten erlaubt den schnellen Überblick über die annotierten Daten.

Die Text Annotation Erweiterung besteht aus und verwendet Komponenten des BTS aus drei Bereichen:

1.  TextAnnotationsPart für die Anzeige von Textannotationen
2.  AnnotationsPart und PassportEditorDialog für die Erstellung und Bearbeitung von Annotationen
3.  Einstellungen zur Definition und Bearbeitung von Eingabeformularen für Annotationen, Definition von Auswahlmenüs und Wertelisten, farbliche Kennzeichnung von Annotationen und Toolbar-Befehle

Im Folgenden werden die Komponenten der drei Bereiche dargestellt und ihre Benutzung zur Erstellung und Bearbeitung von Annotationen erläutert.

Für die allgemeine Dokumentation des BTS möchten wir auf das englische Handbuch zum BTS verweisen. Es ist online frei zugänglich:

www.aaew64.bbaw.de/bts/webhelp

Oder als PDF im BTS, erreichbar über Menü Help > Open Manual (PDF)


## Benutzer ##

Das BTS basiert auf Benutzern, Authentifizierung und Bearbeitungsrechten für die Festlegung, welche Benutzer welche Objekte bearbeiten dürfen. Grundsätzlich wird unterschieden zwischen Leserechten, d.h. das Anzeigen und Lesen von Objekten, und Schreibrechten, die Leserechte einschließen und um das Recht der Bearbeitung und Löschen von Objekten erweitern.

Benutzer des BTS müssen sich für den Zugriff auf Daten anmelden. Möchten sie neue Objekte erstellen oder vorhandene bearbeiten, benötigen sie die entsprechenden Rechte. Für die Einstellung von Rechten, siehe das Manual des BTS.

## Vorbereitung des Arbeitscorpus ##

Das BTS unterstütz sogenanntes stand-off Markup für die Annotationen, d.h. Annotationen zu Texten werden nicht in die Textobjekte selbst hineingeschrieben, sondern als eigenständige Datenbankobjekte gespeichert. Dadurch können auch Benutzer Texte annotieren, die sie selbst nicht bearbeiten dürfen. So kann das Annotieren von Texten zwischen verschiedenen Benutzern, Arbeitsgruppen und Forschungsprojekten hinweg unterstützt werden.

Textcorpusobjekte, zu denen Text und Annotationen zählen, werden im BTS in Textcorpora organisiert. Ein Textkorpus ist ein organisatorischer Teilcorpus innerhalb des verfügbaren Gesamtcorpus im BTS. Für einen Textcorpus lassen sich Benutzerrechte separat definieren. So können Textcorpora die für Arbeitsorganisation innerhalb von Projekten verwendet werden. Textcorpora sind als Datenbankkollektionen umgesetzt, sie sind Teilbereiche der Datenbank und stellen den physischen Speicherort innerhalb der Datenbank dar. Ein Textcorpusobjekt muss daher immer genau einem Textcorpus als Speicherort zugeordnet sein. Über Relationen kann es jedoch mehrere Textcorpora referenzieren und daher auf der inhaltlichen Ebene Teil mehrerer Textcorpora sein.

In der Regel werden die Annotationen zu Texten im BTS in jeweils den Textcorpus gespeichert, in dem auch der annotierte Text selbst gespeichert ist. Wenn keine Schreibrechte auf diesem Textcorpus bestehen, kann auch ein anderer Textcorpus als Arbeitscorpus und damit als Speicherort für die erstellten Annotationen ausgewählt. Dieser Arbeitscorpus kann auch in einem anderen Projekt als dem den zu annotierenden Text enthaltenden Projekt liegen.

### Einstellung des Projekts ###

Für die Einstellung des Projektes, siehe das BTS-Handbuch Kapital General user guide: How to edit a text Unterkapitel Configuration, Preferences

Unter Menü `Preferences` -> `Preferences` und dem Eintrag `Berlin Text System General` -> `Project Settings` kann das Arbeitsprojekt (Main working project) ausgewählt werden. 

Hier können auch die weiteren Projekte ausgewählt werden (Projects to be downloaded), aus denen Daten für die Anzeige geladen werden sollen. Sollen Texte aus anderen Projekten annotiert werden, müssen diese zuvor hier aktiviert werden.

![Project Settings](file:///C:/IT/BTS/Erweiterung_Camilla/img/project_settings.bmp)


### Einstellung des Arbeitscorpus ###

Wenn keine Schreibrechte auf dem Textcorpus bestehen, in dem der zu annotierende Text gespeichert ist, oder aus anderen Gründen die Annotationen in einem anderen Textcorpus gespeichert werden sollen, dann kann ein expliziter Arbeitscorpus ausgewählt werden.

Unter Menü `Preferences` -> `Preferences` und dem Eintrag `Berlin Text System General` -> `Corpus Settings` kann der Arbeitscorpus (Main working corpus) ausgewählt werden.

Hier können auch die weiteren Corpora ausgewählt werden (active corpora), aus denen Daten für die Anzeige geladen werden sollen. Zur Auswahl stehen nur die Textcorpora aus den zuvor aktivierten Projekten und für die der aktuelle Benutzer mindestens Leserechte besitzt. Sollen Texte aus anderen Textcorpora annotiert werden, müssen diese zuvor hier aktiviert werden.

![Corpus Settings](file:///C:/IT/BTS/Erweiterung_Camilla/img/corpus_settings.bmp)

## TextAnnnotionsPart - Ansicht ##

### Überblick und Aufbau ###

Der TextAnnotationsPart zur übersichtlichen Anzeige von Textannotationen zeigt Text satzweise an. Dabei werden Sätze in einer Zeile anzeigt, die Annotationen werden in mehreren Zeilen unter den annotierten Wörtern angezeigt.

![TextAnnotationsPart](file:///C:/IT/BTS/Erweiterung_Camilla/img/textannotationspart.png)

In der Kopfzeile des TextAnnotationsPart kann durch die einzelnen Sätze geblättert werden oder es kann eine Satznummer direkt durch 'Jump' aufgerufen werden.

![Pagination](file:///C:/IT/BTS/Erweiterung_Camilla/img/pagination.bmp)

Die Toolbar enthält Direktbefehle zum Erstellen von Annotationen, Rubra, Glossetexten und Kommentaren. Rechts da neben lassen sich frei definierte Direktbefehle einstellen, mit denen Annotationen mit bestimmten Typen direkt erstellt werden können. Dies erleichtert und beschleunigt das Erstellen von bestimmten, vorher festgelegten Textannotationen.

![Toolbar](file:///C:/IT/BTS/Erweiterung_Camilla/img/toolbar.bmp)

Zum Öffnen des TextAnnotationsPart befindet sich im Menü `Window` der Befehl `Open Text Annotation Part`.

![Open Text Annotation Part](file:///C:/IT/BTS/Erweiterung_Camilla/img/window_menu.bmp)


## Erstellen und Bearbeiten von Annotationen ##

Im folgenden Kapitel werden die wichtigsten Funktionen und Bearbeitunsschritte beim Erstellen und Bearbeiten von Textannotationen Schritt für Schritt erläutert.

Nach dem der Arbeitscorpus wie oben beschrieben eingerichtet ist und der Textcorpus mit dem zu annotierenden Text aktiviert und im CorpusNavigator links angezeigt wird, kann der zu annotierende Text im CorpusNavigator geöffnet werden. Der Text wird dann im EgyTextEditor oder im TextAnnotationsPart angezeigt. Für die Anzeige muss ggfs. in den TextAnnotationsPart gewechselt werden.


### 1. Markieren von Wörtern ###

Zum Annotieren von Wörtern - oder allgemein Satzelementen - müssen diese zunächst durch anklicken ausgewählt werden. Sollen mehrere Satzelemente ausgewählt werden, ist beim Auswählen die STRG bzw. CRTL-Taste gedrückt zu halten. Ausgewählte Wörter werden gelb markiert.

![Auswahl von Wörter](file:///C:/IT/BTS/Erweiterung_Camilla/img/word_selection.png)


### 2. Erstellen einer Annotation ###

Sind die zu annotierenden Wörter bzw. Satzelemente markiert, kann eine Annotation zu diesen erstellt werden. Zum Erstellen einer Annotation kann entweder der allgemeine Befehl `Add Annotation` aus der Toolbar angeklickt werden, der eine Annotation ohne nähere Bestimmung des Annotationstyps erstellt, oder aber es kann ein benutzerdefinierter Annotationsbefehl geklickt werden. Mit Letzterem wird eine Annotation vordefinierten Typs erstellt. Die Typen einer Annotation können jederzeit geändert werden.

![Toolbar Befehle](file:///C:/IT/BTS/Erweiterung_Camilla/img/toolbar_buttons.bmp)


Bei Bedarf können auch die Befehle für Rubrum `Add Rubrum`, Glosse `Add Glosse` oder Kommentar `Add Comment` ausgewählt werden.

![Toolbar weitere Befehle](file:///C:/IT/BTS/Erweiterung_Camilla/img/toolbar_ext.bmp)


Durch das Klicken eines der genannten Befehle zum Erstellen einer Annotation öffnet sich der PassportEditorDialog zum Erstellen und Bearbeiten von Annotationen. Hier muss mindestens eine Name oder Titel für die Annotation eingetragen werden.

![PassportEditorDialog](file:///C:/IT/BTS/Erweiterung_Camilla/img/passporteditordialog.png)


### 3. Festlegen des Types und Subtypes ###

Nach dem Erstellen einer Annotation kann im PassportEditorDialog der Typ und Subtyp der Annotation eingestellt werden - sofern diese nicht bereits durch das Erstellen mittels eines benutzerdefinierten Toolbar-Direktbefehls voreingestellt wurden.

Zum Einstellen eines Typs und Subtyps dienen die beiden Auswahlmenüs.

![Typ und Subtyp](file:///C:/IT/BTS/Erweiterung_Camilla/img/ped_type.png)

Die Werte der Auswahllisten werden in den Einstellungen vorgegeben. Hier ist keine Freitexteingabe möglich.


### 4. Eingabe von Eigenschaften der Annotation ###

Verbunden mit der Einstellung eines Typs einer Annotation ändern sich die voreingestellten Formulare für diesen Typ. Hier werden vordefinierte Formulare vorgestellt.

Für den Annotationstyp: `Lexical Group` gibt es weitere vordefinierte Subtypen, deren Auswahl auch Auswirkungen auf die Eingabeformulare hat.

Wählt man den Annotationstyp `Lexical Group` aus, so erscheint ein neuer Reiter `AEM` im Tabfolder des Editors. Hier befinden sich die vordefinierten Eingabeformulare.

Anmerkung: Die textuellen Eingaben in den folgenden Formularen sind nur Beispiele und nicht voreingestellt oder verpflichtend.

Für die Erläuterung der Reiterkarten `Relations` und `ID` wird auf das BTS-Handbuch verwiesen.


#### Annotationstyp `Lexical Group`, Subtyp `MetaphorRelatedWord` ####

Folgendes Eingabeformular wird dann angezeigt:

![methaphorRelatedWord](file:///C:/IT/BTS/Erweiterung_Camilla/img/methaphorRelatedWord.bmp)


#### Annotationstyp `Lexical Group`, Subtyp `Metaphtonymy` ####

Folgendes Eingabeformular wird dann angezeigt:

![Metaphtonymy](file:///C:/IT/BTS/Erweiterung_Camilla/img/metaphtonymy.bmp)


#### Annotationstyp `Lexical Group`, Subtyp `Metonym` ####

Folgendes Eingabeformular wird dann angezeigt:

![Metaphtonymy](file:///C:/IT/BTS/Erweiterung_Camilla/img/metonym.bmp)


#### Annotationstyp `Lexical Group`, Subtyp `MetaphorFlag`, `Personification`, `SetExpression` oder `ProperName` ####

Folgendes Eingabeformular wird dann angezeigt:

![Metaphtonymy](file:///C:/IT/BTS/Erweiterung_Camilla/img/ped_lexical_group.png)


#### Annotationstyp `ConceptualGroup` ####

Folgendes Eingabeformular wird dann angezeigt:

![Conceptual Group](file:///C:/IT/BTS/Erweiterung_Camilla/img/conceptualGroup.bmp)


#### Annotationstyp `ConceptualGroup2` ####

Folgendes Eingabeformular wird dann angezeigt:

![Conceptual Group 2](file:///C:/IT/BTS/Erweiterung_Camilla/img/conceptualgroup2.bmp)


#### Annotationstyp `ConceptualGroup3` ####

Folgendes Eingabeformular wird dann angezeigt:

![Conceptual Group 3](file:///C:/IT/BTS/Erweiterung_Camilla/img/conceptualgroup3.bmp)


#### Annotationstyp `TextualGroup` ####

Folgendes Eingabeformular wird dann angezeigt:

![TextualGroup](file:///C:/IT/BTS/Erweiterung_Camilla/img/textualgroup.bmp)


### 5. Speichern der Annotation ###

Nach dem alle Einstellungen und Bearbeitungen der Textannotation abgeschlossen sind, kann durch Klicken des Buttons `OK` die Annotation gespeichert werden.


### 6. Auswählen einer Annotation ###

Zum Auswählen einer bereits erstellten Annotation kann diese im TextAnnotationsPart mit der Maus durch Klicken ausgewählt werden.

Zusätzlich können Annotationen über den AnnotationsPart ausgewählt werden. Der AnnotationsPart zeigt alle Annotationen zum geöffneten Text. Eine Annotation, die im AnnotationsPart ausgewählt wurde, wird im AnnotationsPart durch gelben Hintergrund als ausgewählt markiert.

![AnnotationsPart](file:///C:/IT/BTS/Erweiterung_Camilla/img/annotation_parts.bmp)


### 7. Bearbeitern einer Annotation ###

Zum Bearbeiten kann eine ausgewählte Annotation entweder über das Klicken auf das Stift-Symbol im AnnotationsPart geöffnet werden. Beim Öffnen wird die Annotation im PassportEditorDialog angezeigt, ganz wie beim Erstellen einer Annotation.

Eine Annotation kann ebenso durch Doppelklick im TextAnnotationsPart zum Bearbeiten geöffnet werden. Sie öffnet sich dann ebenfalls im PassportEditorDialog.

Nach dem Bearbeiten kann die Annotation durch klicken auf OK wieder gespeichert werden.


### 8. Löschen einer Annotation ###

Zum Löschen einer Annotation muss diese zunächst wie in Punkt 6. ausgewählt werden. Dann kann die markierte Annotation im AnnotationsPart durch Klicken auf das Minus-Symbol in der Toolbar gelöscht werden.

![Delete Annotation](file:///C:/IT/BTS/Erweiterung_Camilla/img/annotation_parts_delete.bmp)


### Filtern von Annotationen ###

Wenn nicht alle Annotationen zu einem Text oder zu einem Satz in einem Text angezeigt werden sollen, so können Annotationen ein- und ausgeblendet bzw. gefiltert werden. Zum Filtern von Annotationen nach Annotationstyp und Subtyp steht eine Funktion im AnnotationsPart zur Verfügung.

![Filter](file:///C:/IT/BTS/Erweiterung_Camilla/img/filter.bmp)


## Einstellungen ##

Viele der vorstehend beschriebenen Funktionen beruhen auf benutzerdefinierten Einstellungen und können je nach Bedarf angepasst werden. In vielen Fällen ist das Anpassen oder Erweitern auch zu späteren Zeitpunkten möglich.


### Einstellungen des TextAnnotationPart ###

Beim TextAnnoationsPart lässt sich einstellen, ob in den Boxen für die Annotationen auch alle Eigenschaften der Annotationen angezeigt werden sollen. Dies erlaubt einen schnellen Überlick, kann die Anzeige jedoch auch unübersichtlich machen.

Unter Menü `Preferences` -> `Preferences...` und dem Punkt `Text Annotation Part` kann diese Funktion ein- und ausgeschaltet werden. Zudem lassen sich Tooltip-Informationen mit allen Eigenschaften der Annotationen aktivieren.

![Text Annotation Settings](file:///C:/IT/BTS/Erweiterung_Camilla/img/text_annotation_settings.bmp)


### Einstellungen der Annotations Farben und Shortcuts###

Die farbliche Hinterlegung der Annotationen lässt sich je nach Typ und Subtyp einer Annotation einstellen. Hierzu gibt es Einstellungsmöglichkeiten unter Menü `Preferences` -> `Preferences...` und dem Punkt `Text Annotation Settings`. Eine Einstellungen je Annotationstyp/subtyp zu erstellen, bitte `Add Annotation Styling` klicken.

![Annotation Styling](file:///C:/IT/BTS/Erweiterung_Camilla/img/text_annotation_settings_color.bmp)


### Einstellungen der Formulare ###

Zunächst ist die Auswahl der richtigen Konfigurationen wichtig. Unter Menü `Preferences` -> `Preferences...` und dem Punkt `Configuration` können verschiedene Konfigurationen ausgewählt werden. Hier wird die Konfiguration `AEM Configuration` verwendet.

Unter Menü `Preferences` -> `Edit Configuration` kann der ConfigurationDialog geöffnet werden und könnend ie Konfigurationen angepasst werden. Die Formulare können bearbeitet werden, indem die jeweiligen Knoten im Konfigurationsbaum ausgewählt werden. Neue Eingabefelder können hinzugefügt werden, dann könnend die Felder ausgewählt und angepasst werden.

![Configuration AEM](file:///C:/IT/BTS/Erweiterung_Camilla/img/configuration_aem_ed.png)


### Einstellungen der Auswahllisten ###

Die Werte der Auswahrlisten lassen sich auch im ConfigurationDialog bearbeiten. Unter `Custom Entries` können vorhandene Listen bearbeitet oder neue erstellt werden.

![Custom Entries](file:///C:/IT/BTS/Erweiterung_Camilla/img/aem_custom_values.bmp)

Die Verknüpfung von Eingabemasken bzw. Widgets mit benutzerdefinierten Wertelisten geschied über die Reiterkarte `Owner and Related Objects`.

![Select Custum values](file:///C:/IT/BTS/Erweiterung_Camilla/img/aem_select_custom_values.bmp)


## Voreingestellt Preferences ##

Alle Einstellungen in den Konfigurationen werden automatisch zwischen verschiedenen Installationen synchronosiert, genauso, wie die Datenbanken synchronisiert werden - und natürlich nur insofern eine Internetverbindung und eine Anbindung an einen zentralen Server besteht.

Die Einstellungen unter dem Menü `Preferences...` sind demgegenüber lokal und werden nie synchronisiert. Um diese Einstellungen zur Installation anzupassen, können bestimmte Werte in die BTS-Preferences-Dateien manuell kopiert werden.

In die Datei: `workspace\.metadata\.plugins\org.eclipse.core.runtime\.settings\org.bbaw.bts.app.prefs`

`active_configuration=aemconfig`


`active_projects=aem|aaew`


`main_corpus_key=aem_corpus_annotations`


`main_project_key=aem`


`pref_corpus_activate_main_corpus_selection=true`



