# Aktuelle Trends der IKT

Herzlich willkommen zur Veranstaltung **Aktuelle Trends der IKT**! 

### Grober Inhalt

Wir beschäftigen uns dieses Semester mit *Progressive Web Apps (PWA)*. Dieser Begriff ist 2015 bei Google entstanden. Progressive Web Apps bieten installierbare nativen Apps ähnliche Nutzererfahrungen sowohl auf dem Desktop als auch auf dem Smartphone, sind aber Webanwendungen, die im Browser laufen, also zum World Wide Web gehören. Typische Eigenschaften von Progressive Web Apps sind die Einbindung von Kamera und Mikrofon, dem eigenen Standort sowie die Fähigkeit, (zumindest teilweise) offline ausführbar zu sein. 

Nachfolgend der vorläufige Wochenplan (wird eventuell angepasst). Die Vorlesungsvideos finden Sie darunter für die einzelnen Wochen (unter [**Inhalte**](http://freiheit.f4.htw-berlin.de/ikt/#inhalte)).

| | Woche | Themen (Vorlesung) | Übung | Aufgabe (Stand) | Abgabe Übung bis | 
|-|-------|--------------------|-------|-----------------|------------------|
| 1. | 12.-16.04.2021 | Einführung und Organisatorisches | - | - | - | 
| 2. | 19.-23.04.2021 | Grundgerüst und Application Manifest | Übung 1 | - | 30.04.2021 | 
| 3. | 26.-30.04.2021 | Service workers | Übung 2 | - | 07.05.2021 | 
| 4. | 03.-07.05.2021 | Promises und Fetch API | Übung 3 | - | 14.05.2021 | 
| 5. | 10.-14.05.2021 | Service workers und Caching | Übung 4 | - | 21.05.2021 | 
| 6. | 17.-21.05.2021 | Caching II | Übung 5 | - | 28.05.2021 | 
| 7. | 24.-28.05.2021 | Caching dynamische Daten mit IndexDB | Übung 6 | - | 04.06.2021 | 
| 8. | 31.-04.06.2021 | Responsive Webdesign | Übung 7 | - | 11.06.2021 | 
| 9. | 07.-11.06.2021 | Hintergrundsynchronisation  | Übung 8 | - | 18.06.2021 | 
| 10. | 14.-18.06.2021 | Push-Notifikationen | Übung 9 | - | 25.06.2021 | 
| 11. | 21.-25.06.2021 | Media API (Kamera) | Übung 10 | - | 02.07.2021 | 
| 12. | 28.-02.07.2021 | Geolocation  | - | - | - |
| 13. | 05.-09.07.2021 | automatisierte Service worker Verwaltung | - | - | - |
| 14. | 12.-16.07.2021 | SPAs und PWAs mit Angular | - | - | - |
|  |  |  |  | Abgabe 1.PZ 16.07.2021 | - |
|  |  |  |  | Abgabe 2.PZ 01.10.2021 | - |

### Organisatorisches 

Zur erfolgreichen Durchführung der Veranstaltung müssen Sie die Übungen lösen und zu den jeweiligen Fristen per Git auf einen Server (GitHub oder GitLab) laden. Am Ende des Semesters ist eine Aufgabe abzugeben. Diese Aufgabe wird bewertet. Die Bewertung entspricht dann der Modulnote. 

Hier sind die Übungen beschrieben, die Sie in jeder Woche ausführen sollen. Damit Sie dies erfolgreich erledigen können, ist jeweils angegeben, welche Themen Sie dafür durcharbeiten müssen. Das Durcharbeiten der jeweiligen Themen entspricht jeweils einer Vorlesung. Diese wird also selbständig durchgeführt. 

Für die Kommunikation untereinander verwenden wir [**Slack**](https://slack.com/intl/de-de/). Dort können Sie alle inhaltlichen und organisatorischen Fragen stellen. Ich fände es gut, wenn ich dort möglichst wenig Fragen - zumindest die inhaltlichen - beantworten müsste, sondern eine Art internes **Diskussionsforum** entsteht. Es ist sehr gewünscht, dort Fragen zu stellen und noch mehr gewünscht, diese **von Ihnen dort beantwortet** zu sehen. Damit wäre allen geholfen und ich kann besser erkennen, wo noch Nachhol- bzw. Erläuterungsbedarf bei den meisten besteht. Außerdem lernen Sie beim Beantworten der Fragen nochmals deutlich mehr. Das wäre super, wenn das klappt!

### Inhalte


##### Woche 1 (Grundgerüst)

??? question "Woche 1 - Grundgerüst"

	- eigentlich wollten wir diese Woche auch das [Application Manifest](./manifest/#web-app-manifest) machen, aber da wir am Mittwoch an einem Antirassismus-Seminar teilnehmen und somit die Vorlesung ausfällt, fangen wir ganz langsam an und betrachten nur das [Grundgerüst](./grundgeruest/#grundgerust-unserer-pwa). Dazu auch folgendes Video: 
	<iframe src="https://mediathek.htw-berlin.de/media/embed?key=9acae2bf623912843d1298721c67867a&width=720&height=405&autoplay=false&autolightsoff=false&loop=false&chapters=false&related=false&responsive=false&t=0" data-src="" class="iframeLoaded" width="720" height="405" frameborder="0" allowfullscreen="allowfullscreen" allowtransparency="true" scrolling="no"></iframe>
	- Bearbeiten Sie bitte außerdem [Übung 1](./uebungen/#ubung-1-grundgerust). Fragen dazu klären wir in der [Übung am Donnerstag um 12:15 Uhr](https://htw-berlin.zoom.us/j/95912146800?pwd=UklCbGNicUh6L29yaGpuNzhTaDBXZz09). Die Übung um 9:45 Uhr am Donnerstag findet nicht statt, da um diese Zeit das gemeinsame Plenum zum Thema *Design Research* in der Veranstaltung *Usability* stattfindet. 


##### Woche 2 (Manifest)

??? question "Woche 2 - Manifest"

	- Diese Woche wird unsere App mithilfe des [Application Manifest](./manifest/#web-app-manifest) **installierbar**. Arbeiten Sie bitte den [Abschnitt dazu](./manifest/#web-app-manifest) durch. Dazu gibt es folgendes Video: 
	<iframe src="https://mediathek.htw-berlin.de/media/embed?key=247bb388ae29a4d849a3fcff5fae95db&width=720&height=450&autoplay=false&autolightsoff=false&loop=false&chapters=false&related=false&responsive=false&t=0" data-src="" class="iframeLoaded" width="720" height="450" frameborder="0" allowfullscreen="allowfullscreen" allowtransparency="true" scrolling="no"></iframe>
	- Bearbeiten Sie bitte zu diesem Thema [Übung 2](./uebungen/#ubung-2-web-app-manifest). Leider müssen diesen Donnerstag aufgrund einer großen Veranstaltung in unserem Forschungsprojekt **beide Übungen entfallen** - tut mir wirklich leid, wird aber die kommenden Wochen (hoffentlich!!) besser! Fragen müssen wir deshalb leider über Slack klären.  


##### Woche 3 (Promises und Fetch API)

??? question "Woche 3 - Promises und Fetch API"

	- Diese Woche betrachten wir den Lebenszyklus eines Service Workers, schauen uns Promises und die Fetch API an. In der Vorlesung wird ein Video erstellt, das hier hochgeladen wird. Die relevanten Abschnitte im Skript sind [Service Workers](./serviceworker/#service-workers) und [Promises und die Fetch-API](./promises/#promises-und-die-fetch-api).
	- Bearbeiten Sie bitte zu diesem Thema [Übung 3](./uebungen/#ubung-3-promises-und-fetch-api). 
	- Video zur Vorlesung am 05.05.2021
		<iframe src="https://mediathek.htw-berlin.de/media/embed?key=71d02c5d395a874c9b2b4821a140dc7f&width=720&height=389&autoplay=false&autolightsoff=false&loop=false&chapters=false&related=false&responsive=false&t=0" data-src="" class="iframeLoaded" width="720" height="389" frameborder="0" allowfullscreen="allowfullscreen" allowtransparency="true" scrolling="no"></iframe>
	- Sourcecode zur Vorlesung am 05.05.2021 [hier zum Herunterladen](./files/03_promise.zip)
