<!--

author:   Sebastian Zug & André Dietrich
email:    zug@ovgu.de   & andre.dietrich@ovgu.de
version:  0.0.1
language: de
narrator: Deutsch Female

import: https://raw.githubusercontent.com/liaScript/rextester_template/master/README.md
import: https://raw.githubusercontent.com/liaScript/WebDev_template/master/README.md
import: https://raw.githubusercontent.com/liascript-templates/plantUML/master/README.md
-->

# Vorlesung Softwareentwicklung - 10 - UML und OOP

--------------------------------------------------------------------
Link auf die aktuelle Vorlesung im Versionsmanagementsystem GitHub

https://github.com/liaScript/CsharpCourse/blob/master/10_UMLI.md

Die interaktive Form ist unter diese Link zu finden ->
[LiaScript Vorlesung 10](https://liascript.github.io/course/?https://raw.githubusercontent.com/liaScript/CsharpCourse/master/10_UMLI.md#1)

---------------------------------------------------------------------

**Wie weit sind wir schon gekommen?**

c# Schlüsselwörter:

| abstract    | as       | base     |`bool`      |`break`     |`byte`     |
|`case`       |`catch`   | char     |`checked`   |`class`     | const     |
|`continue`   |`decimal` | default  | delegate   |`do`        |`double`   |
|`else`       |`enum`    | event    | explicit   | extern     |`false`    |
|`finally`    | fixed    |`float`   |`for`       |`foreach`   |`goto`     |
|`if`         | implicit | in       |`int`       | interface  |`internal` |
| is          | lock     |`long`    |`namespace` |`new`       | null      |
| object      | operator |`out`     | override   |`params`    |`private`  |
| protected   |`public`  | readonly |`ref`       |`return`    |`sbyte`    |
| sealed      |`short`   | sizeof   | stackalloc |`static`    |`string`   |
|`struct`     |`switch`  |`this`    |`throw`     |`true`      |`try`      |
| typeof      |`uint`    |`ulong`   |`unchecked` | unsafe     |`ushort`   |
|`using`      | virtual  |`void`    | volatile   |`while`     |           |


Auf die Auführung der kontextabhängigen Schlüsselwörter wie `where` oder
`ascending` wurde hier verzichtet.

---

## Kontrollfragen

*1. Welche Unterschiede zeigen abstrakte Klassen und Interfaces unter C#*

--------------------------------------------------------------------

*2. Warum verzichten einige Programmiersprachen auf die Differenzierung zwischen Klassen und Interfaces?*

---------------------------------------------------------------------

## 1. Ausgangspunkt

                                       {{0}}
****************************************************************************

Kunde TU Freiberg: *Entwickeln Sie für mich ein webbasiertes System, mit dem Sie die Anmeldung und Bewertung von Prüfungsleistung erfassen.*

Welche Fragen sollten Sie dem Kunden stellen, bevor Sie sich daran machen und munter Code schreiben?

****************************************************************************
                                        {{1}}
****************************************************************************
![OOPGeschichte](/img/10_UML/cartoon-projekte.png)<!-- width="80%" --> [Possel](#7)

Wie verzahnen wir den Entwicklungsprozess? Wie können wir sicherstellen,
dass am Ende die erwartete Anwendung realisiert wird?

****************************************************************************

                                         {{2}}
****************************************************************************
<!--
style="width: 100%; max-width: 560px; display: block; margin-left: auto; margin-right: auto;"
-->
````````````

         +------------------------------------------------------>   Zeit
         |
         |      Analyse                             Abnahmetest
         |          \                                   ^
         |           v                                 /
         |        Grobentwurf                   Systemtests
         |             \                             ^
         |              v                           /
         |           Feinentwurf             Integrationstests      
 Detail- |                \                       ^
 grad    |                 v                     /
         |             Implementierung  --> Modultests
         |
         v    
````````````

> Das V-Modell ist ein Vorgehensmodell, das ähnlich dem Wasserfallmodell, den Softwareentwicklungsprozess in Phasen  organisiert. Zusätzlich zu den Entwicklungsphasen definiert das V-Modell auch das Evaluationsphasen, in welchen den einzelnen Entwicklungsphasen Testphasen gegenüber gestellt werden.

vgl. zum Beispiel [Link](https://www.johner-institut.de/blog/iec-62304-medizinische-software/v-modell/)

Achtung: Das V-Modell ist nur eine Variante eines Vorgehensmodells, moderne
Entwicklungen stellen eher agile Methoden in den Vordergrund.

vgl. zum Beispiel [Link](https://entwickler.de/online/agile/agile-methoden-einfuehrung-209035.html)

****************************************************************************

## 2. Unified Modeling Language

> Die Unified Modeling Language, kurz UML, dient zur Modellierung, Dokumentation , Spezifikation und Visualisierung komplexer Softwaresysteme unabhängig von deren Fach- und Realsierungsgebiet. Sie liefert die Notationselemente gleichermaßen fpr statische und dynamische Modelle zur Analyse, Design und Architektur und unterstützt insbesondere objektorientierte Vorgehensweisen. [Jeckle]

UML ist heute die dominierende Sprache für die Softwaresystem-Modellierung. Der erste Kontakt zu UML besteht häufig darin, dass Diagramme in UML im Rahmen von Softwareprojekten zu erstellen, zu verstehen oder zu beurteilen sind:

+ Projektauftraggeber und Fachvertreter prüfen und bestätigen zum Beispiel Anforderungen an ein System, die Wirtschaftsanalytiker bzw. Business Analysten in Anwendungsfalldiagrammen in UML festgehalten haben;
+ Softwareentwickler realisieren Arbeitsabläufe, die Wirtschaftsanalytiker bzw. Business Analysten in Zusammenarbeit mit Fachvertretern in Aktivitätsdiagrammen beschrieben haben;
+ Systemingenieure implementieren, installieren und betreiben Softwaresysteme basierend auf einem Implementationsplan, der als Verteilungsdiagramm vorliegt.

UML dabei Bezeichner für die meisten bei einer Modellierung wichtigen Begriffe und legt mögliche Beziehungen zwischen diesen Begriffen fest. UML definiert weiter grafische Notationen für diese Begriffe und für Modelle statischer Strukturen und dynamischer Abläufe, die man mit diesen Begriffen formulieren kann.

> **Merke:**  Die grafische Notation ist jedoch nur ein Aspekt, der durch UML geregelt wird. UML legt in erster Linie fest, mit welchen Begriffen und welchen Beziehungen zwischen diesen Begriffen sogenannte Modelle spezifiziert werden.

Was ist UML nicht:

+ vollständige, eindeutige Abbildung aller Anwendungsfälle
+ keine Programmiersprache
+ keine rein formale Sprache
+ kein vollständiger Ersatz für textuelle Beschreibungen
+ keine Methode oder Vorgehensmodell [Jeckle]

### Geschichte

UML (aktuell UML 2.5) ist durch die Object Management Group (OMG) als auch die ISO (ISO/IEC 19505 für Version 2.4.1) genormt.

![OOPGeschichte](/img/10_UML/OO-historie.png)<!-- width="70%" --> [WikiUMLHistory](#7)


### UML Werkzeuge

* Tools zur Modellierung - Unterstützung des Erstellungsprozesses, Überwachung der Konformität zur graphischen Notation der UML

    *Herausforderungen:* Transformation und Datenaustausch zwischen unterschiedlichen Tools

* Quellcoderzeugung - Generierung von Sourcecode aus den Modellen

    *Herausforderungen:* Synchronisation der beiden Repräsentationen, Abbildung wiedersprüchlicher Aussagen aus verschiedenen Diagrammtypen

    (Beispiel mit Visual Studio folgt am Ende der Vorlesung.)

* Reverse Engineering / Dokumentation - UML-Werkzeug bilden Quelltext als Eingabe liest auf entsprechende UML-Diagramme und Modelldaten ab

    *Herausforderungen:* Abstraktionskonzept der Modelle führt zu verallgemeinernden Darstellungen, die ggf. Konzepte des Codes nicht reflektieren.

![OOPGeschichte](/img/10_UML/Doxygen.png)<!-- width="80%" --> [WikiDoxygen](#7)


**Darstellung von UML im Rahmen dieser Vorlesung**

Die Vorlesungsunterlagen der Veranstaltung "Softwareentwicklung" setzen auf die domainspezifische Beschreibungssprache plantUML auf, die verschiedene Aspekte in einer

http://plantuml.com/de/

```ascii PlantUMLClasses
@startuml
class Car

Driver - Car : drives >
Car *- Wheel : have 4 >
Car -- Person : < owns

@enduml
```
@plantUML.eval


```ascii PlantUMLTimings
@startuml
robust "Web Browser" as WB
concise "Web User" as WU

@0
WU is Idle
WB is Idle

@100
WU is Waiting
WB is Processing

@300
WB is Waiting
@enduml
```
@plantUML.eval

## 3. Diagramm-Typen

![OOPGeschichte](/img/10_UML/UML-Diagrammhierarchie.png)<!-- width="90%" --> [WikiUMLHistory](#7)

| Diagrammtyp                  | Zentrale Frage                                                                                                           |
| ---------------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| Klassendiagramm              | Welche Klassen bilden das Systemverhalten ab und in welcher Beziehung stehen diese?                                      |
| Paketdiagramm                | Wie kann ich mein Modell in Module strukturieren?                                                                        |
| Objektdiagramm               | Welche Instanzen bestehen zu einem bestimmten Zeitpunkt im System?                                                       |
| Kompositionsstrukturdiagramm | Welche Elemente sind Bestandteile einer Klasse, Komponente, eines Subsystems?                                            |
| Komponentendiagramm          | Wie lassen sich die Klassen zu wiederverwendbaren Komponenten zusammenfassen und wie werden deren Beziehungen definiert? |
| Verteilungsdiagramm          | Wie sieht das Einsatzumfeld des Systems aus?                                                                             |

| Diagrammtyp                    | Zentrale Frage                                                                                |
| ------------------------------ | --------------------------------------------------------------------------------------------- |
| Use-Case-Diagramm              | Was leistet mein System überhaupt? Welche Anwendungen müssen abgedeckt werden?                |
| Aktivitätsdiagramm             | Wie lassen sich die Stufen eines Prozesses beschreiben?                                       |
| Zustandsautomat                | Welche Abfolge von Zuständen wird für eine eine Sequenz von Einganginformationen realisiert   |
| Sequenzdiagramm                | Wer tauscht mit wem welche Informationen aus? Wie bedingen sich lokale Abläufe untereinander? |
| Kommunikationsdiagramm         | Wer tauscht mit wem welche Informationen aus?                                                 |
| Timing-Diagramm                | Wie hängen die Zustände verschiedener Akteure zeitlich voneinander ab?                        |
| Interaktionsübersichtsdiagramm | Wann läuft welche Interaktion ab?                                                             |  

[Jeckle]

**Begrifflichkeiten**

Ein UML-Modell ergibt sich aus der Menge aller seiner Diagramme. Entsprechend
werden verschiedene Diagrammtypen genutzt um unterschiedliche Perspektiven auf
ein realweltliches Problem zu entwickeln.

![Modelle](http://www.plantuml.com/plantuml/png/JSj1oi9030NW_PmYpFA7ARG7-Ed2fLrwW3WJsq3IWIIzlwAYhXxlVRpP0oqEbIHq2uWEnkiMqDYe1lSzRTm8bFHAvgzIsQfGIbNG7V9bEPUbDnB9W0xFTVh54-DggFhbyNsU88yPIlb_v33yvO_EjBT3vGu0)<!-- width="40%" --> [ModelvsDiagramm.plantUML]

### Use-Case Diagramm

> Das Anwendungsfalldiagramm (Use-Case Diagramm) abstrahiert das erwartete
> Verhalten eines Systems und wird dafür eingesetzt, die Anforderungen an ein
> System zu spezifizieren.

Ein Anwendungsfalldiagramm stellt keine
Ablaufbeschreibung dar! Diese kann stattdessen mit einem Aktivitäts-, einem
Sequenz- oder einem Kollaborationsdiagramm (ab UML 2.x Kommunikationsdiagramm)
dargestellt werden.

**Basiskonzepte**

Elemente:

+ Systemgrenzen werden durch Rechtecke gekennzeichnet.
+ Akteure werden als „Strichmännchen“ dargestellt, dies können sowohl Personen (Kunden, Administratoren) als auch technische Systeme sein (manchmal auch ein Bandsymbol verwendet). Sie ordnen den Symbolen Rollen zu
+ Anwendungsfälle werden in Ellipsen dargestellt. Sie müssen beschrieben werden (z. B. in einem Kommentar oder einer eigenen Datei).
+ Beziehungen zwischen Akteuren und Anwendungsfällen müssen durch Linien gekennzeichnet werden.

![Modelle](http://www.plantuml.com/plantuml/png/RL11Rkf03DtFAInMi63n-HUWeAverGLIkpQ9IKPndCZZgGHLRzDZTCV5EY4f6gIk_6I_Pp-_TJ1KYoqxfgE1TQ2-gWrAhrIOxyI5nakFYYtqM3HOqTvEJ32CKIecXuLr2hievI_Urrt_Z9AuEdMU1ko3kPiCNeIzK4XK-700ymSrtn33WO8HCya2C40CjCL0_nmaoYQDK4eeenPrY4LzJrev66t0SlbdRtv5KgAHmEKhOPL5JiYkpTzGIP9LEdG6_P6f6gubKlxTP8gOerHmZYsyaeR1utkd1rBoDgbk2NowB8JP1gK9fs3Kml7ohV2uNUvGasWsFBQ_JbPkghd5VCaO9MpeZ3MFspBvVpVLExbRavInvHy0)<!-- width="70%" --> [UseCase.plantUML]

**Verfeinerung**

Use-Case Diagrammer erlaube die Abstraktion von Elementen auf der Basis von Generalisierungen. So können Akteure von einander erben und redundante Beschreibungen von Verhalten über `<<extend>>` oder `<<include>>` (unter bestimmten Bedingungen) erweitert werden.

![Modelle](img/10_UML/UseCase.png)<!-- width="70%" --> [Jeckle Seite 240](#7)

|                | <img src="https://raw.githubusercontent.com/liaScript/CsharpCourse/master/img/10_UML/UseCaseInclude.png" height="42">                             | <img src="https://raw.githubusercontent.com/liaScript/CsharpCourse/master/img/10_UML/UseCaseExtend.png" height="42">         |
| -------------- | ------------------------------------------------ | ------------------------------------------------ |
|                | `<<include>>` Beziehung                          | `<<extend>>` Beziehung                           |
| Bedeutung      | Ablauf von A schließt den Ablauf von B immer ein | Ablauf von A kann optional um B erweitert werden |
| Anwendung      | Hierachische Zerlegung                           | Abbildung von Sonderfällen                       |
| Abhängigkeiten | A muss B bei der Modellierung berücksichtigen    | Unabhängige Modellierung möglich                 |


**Anwendungsfälle**

+ Darstellung der wichtigsten Systemfunktionen
+ Austausch mit dem Anwender und dem Management auf der Basis logischer, handhabbarer Teile
+ Dokumentation des Systemüberblicks und der Außenschnittstellen
+ Indentifikation von Anwendungsfällen

**Vermeiden Sie ...**

+ ... eine zu detaillierte Beschreibung von Operationen und Funktionen
+ ... nicht funktionale Anforderungen mit einem Use-Case abbilden zu wollen
+ ... Use-Case Analysen aus Entwicklersicht durchzuführen
+ ... zu viele Use-Cases in einem Diagramm abzubilden (max. 10)

## Und weiter geht's

... mit Aktivitäts-, Sequenz und Klassendiagrammen in der nächsten Woche.

## Anhang

**Referenzen**

[Possel] Heiko Possel, https://www.programmwechsel.de/lustig/management/schaukel-baum.html

[Jeckle]  Mario Jeckle, Christine Rupp, Jürgen Hahn, Barbara Zengler, Stefan Queins, UML 2 glasklar, Hanser Verlag, 2004

[WikiUMLHistory] https://commons.wikimedia.org/w/index.php?curid=7892951, Autor GuidoZockoll, Mitarbeiter der oose.de Dienstleistungen für Innovative Informatik GmbH -
derivative work: File:OO-historie.svg : AxelScheithauer, oose.de Dienstleistungen für Innovative Informatik GmbH -
derivative work: Chris828 (talk) - File:Objektorientieren methoden historie.png and File:OO-historie.svg, CC BY-SA 3.0

[WikiSequenceDiagram] By Coupling_loss_graph.svg - File:CheckEmail.png, CC BY-SA 3.0, https://commons.wikimedia.org/w/index.php?curid=20544977

[WikiUMLDiagrammTypes] https://upload.wikimedia.org/wikipedia/commons/thumb/d/da/UML-Diagrammhierarchie.svg/1200px-UML-Diagrammhierarchie.svg.png, Autor "Stkl"- derivative work: File: UML-Diagrammhierarchie.png: Sae1962, CC BY-SA 4.0

[WikiDoxygen] https://commons.wikimedia.org/w/index.php?curid=24966914, Doxygen-Beispielwebseite, Autor Der Messer - Eigenes Werk, CC BY-SA 3.0

[StackOverFlow] http://oi43.tinypic.com/2s7dr8y.jpg, StackOverFlow Forum, Autor unbekannt


**Autoren**

Sebastian Zug, André Dietrich
