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
| 5. | 10.-14.05.2021 | Service workers und Caching | - | - | 21.05.2021 | 
| 6. | 17.-21.05.2021 | Entwicklungsinfrastruktur | Übung 4 | - | 28.05.2021 | 
| 7. | 24.-28.05.2021 | Datenbank und Backend | Übung 5 | - | 04.06.2021 | 
| 8. | 31.-04.06.2021 | Frontend mit Backend-Anbindung | Übung 6 | - | 11.06.2021 | 
| 9. | 07.-11.06.2021 | Caching dynamische Daten mit IndexDB | Übung 7 | - | 18.06.2021 | 
| 10. | 14.-18.06.2021 | Hintergrundsynchronisation | - | Datenbank | - | 
| 11. | 21.-25.06.2021 | Push-Notifikationen | - | Backend | - | 
| 12. | 28.-02.07.2021 | Kamera und Geolocation | - | Frontend | - |
|  |  |  |  | Abgabe 1.PZ 21.07.2021 | - |
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


##### Woche 4 (Caching)

??? question "Woche 4 - Caching"

	- Diese Woche wird die App mithilfe von [Caching](./caching/#caching-mit-service-workern) auch offline nutzbar.
	- Die Übung entfällt diese Woche wegen des Feiertages. Arbeiten Sie aber das [Caching](./caching/#caching-mit-service-workern)-Kapitel durch. 
	- Video zur Vorlesung am 12.05.2021
		<iframe src="https://mediathek.htw-berlin.de/media/embed?key=bf498f35fe78e01a22d5fa909d4c4be8&width=720&height=389&autoplay=false&autolightsoff=false&loop=false&chapters=false&related=false&responsive=false&t=0" data-src="" class="iframeLoaded" width="720" height="389" frameborder="0" allowfullscreen="allowfullscreen" allowtransparency="true" scrolling="no"></iframe>
	- Sourcecode zur Vorlesung am 12.05.2021 [hier zum Herunterladen](./files/04_caching.zip)


##### Woche 6 (Datenbank und Backend)

??? question "Woche 6 - Datenbank und Backend"

	- Diese Woche bereiten wir zunächst die nächsten Kapitel vor. Dazu benötigen wir eine [Datenbank und ein Backend](./backend/#rest-server), das an die Datenbank angebunden ist. 
	- In der [Übung](./uebungen/#ubung-5-backend) soll das Backend um eine weitere Funktion erweiteret werden. 
	- Video zur Vorlesung am 26.05.2021
		<iframe src="https://mediathek.htw-berlin.de/media/embed?key=a6e060a195129540a18a7be89a3738e7&width=720&height=450&autoplay=false&autolightsoff=false&loop=false&chapters=false&related=false&responsive=false&t=0" data-src="" class="iframeLoaded" width="720" height="450" frameborder="0" allowfullscreen="allowfullscreen" allowtransparency="true" scrolling="no"></iframe>


##### Woche 7 (Frontend und Backend-Anbindung)

??? question "Woche 7 - Frontend und Backend-Anbindung"

	- Diese Woche erstellen wir uns mithilfe von Angular ein [Frontend](./frontend/#frontend) und binden dieses an das Backend an. Damit wird es uns möglich, Daten in ein Formular einzugeben und diese Daten werden in der Datenbank gespeichert.  
	- In der [Übung](./uebungen/#ubung-6-frontend) soll das Frontend um eine weitere Funktion und eine Komponente erweiteret werden. 
	- Video zur Vorlesung am 02.06.2021
		<iframe src="https://mediathek.htw-berlin.de/media/embed?key=63500e11ed3c99c726ac2a962f710a9f&width=720&height=450&autoplay=false&autolightsoff=false&loop=false&chapters=false&related=false&responsive=false&t=0" data-src="" class="iframeLoaded" width="720" height="450" frameborder="0" allowfullscreen="allowfullscreen" allowtransparency="true" scrolling="no"></iframe>




##### Woche 8 (IndexedDB)

??? question "Woche 8 - IndexedDB"

	- Diese Woche machen wir uns mit der [IndexedDB](./indexeddb/#indexeddb) vertraut und speichern dynamische Daten (die `Posts`-Datensaätze) in die IndexedDB, um diese auszulesen, falls die Anwendung offline ist und somit das Backend nicht verfügbar.   
	- In der [Übung](./uebungen/#ubung-7-indexeddb) soll die Verwaltung der IndexedDB um eine weitere Funktion erweiteret werden. 
	- Video zur Vorlesung am 09.06.2021
		<iframe src="https://mediathek.htw-berlin.de/media/embed?key=531c0ff5c9765951731a6e27fe41a11e&width=720&height=450&autoplay=false&autolightsoff=false&loop=false&chapters=false&related=false&responsive=false&t=0" data-src="" class="iframeLoaded" width="720" height="450" frameborder="0" allowfullscreen="allowfullscreen" allowtransparency="true" scrolling="no" aria-label="media embed code" style=""></iframe>



##### Woche 9 (Hintergrundsynchronisation)

??? question "Woche 9 - Hintergrundsynchronisation"

	- Diese Woche machen wir uns mit der [Hintergrundsynchronisation](./backgroundsync/#hintergrundsynchronisation) vertraut. Diese verwenden wir, um Daten, die wir in der Webanwendung erstellt oder eingegeben haben, an das Backend zu senden. Die zu sendenden Daten werden zunächst in der IndexedDB gesichert und verbleiben dort so lange, bis die Übersendung an das Backend erfolgreich war.    
	- Eine neue Übung gibt es nicht (mehr), sondern Sie können schonmal mit der Semesteraufgabe beginnen. 
	- Video zur Vorlesung am 16.06.2021
		<iframe src="https://mediathek.htw-berlin.de/media/embed?key=aafa75ddca04b5a4e5fda406772777fe&width=720&height=389&autoplay=false&autolightsoff=false&loop=false&chapters=false&related=false&responsive=false&t=0" data-src="" class="iframeLoaded" width="720" height="389" frameborder="0" allowfullscreen="allowfullscreen" allowtransparency="true" scrolling="no" aria-label="media embed code" style=""></iframe>



##### Woche 10 (Push-Benachrichtigungen)

??? question "Woche 10 - Push-Benachrichtigungen"

	- Diese Woche machen wir uns mit der [Push-benachrichtigung](./pushnotes/#push-notifications) vertraut. Diese verwenden wir, um die Nutzerinnen zu informieren, dass es Änderungen (Updates/Aktuelles) in der Webanwendung gibt. Die Nutzerinnen werden so an die Anwendung gebunden, denn Push-Notifications erhöhen das Interesse daran, die Anwendung erneut zu öffnen.     
	- Eine neue Übung gibt es nicht (mehr), sondern Sie können (schonmal) mit der Semesteraufgabe beginnen/weitermachen. 
	- Video zur Vorlesung am 23.06.2021
		<iframe src="https://mediathek.htw-berlin.de/media/embed?key=bd60899d214c44a0a15987921ddcf908&width=720&height=450&autoplay=false&autolightsoff=false&loop=false&chapters=false&related=false&responsive=false&t=0" data-src="" class="iframeLoaded" width="720" height="450" frameborder="0" allowfullscreen="allowfullscreen" allowtransparency="true" scrolling="no" aria-label="media embed code" style=""></iframe>
		


##### Woche 11 (Kamera und Geolocation)

??? question "Woche 11 - Kamera und Geolocation"

	- Diese Woche machen wir uns mit der Anwendung der [Kamera und der Geolocation-API](./devices/#geratezugriffe) vertraut. Wir streamen Videos und nehmen Fotos auf. Diese speichern wir im Backend. Wir haben dadurch nun auch aus der *HTW-Insta*-App die Möglichkeit, *Posts* zu speichern. Außerdem ermitteln wir mithilfe der Geolocation-API unseren aktuellen Standort. Diese Art der Gerätezugriffe war lange aus Webanwendungen nicht möglich, ist nun aber mit zunehmend mehr APIs und Browserunterstützung auch für (progressive) Webanwendungen verfügbar.     
	- Es gibt auch noch einen kurzen Abschnitt [Zusammenfassung](./zusammenfassung/#zusammenfassung), der ein kurzes Tutorial enthält, wie eine Angular-Anwendung *progressive* gestaltet werden kann und auch einen kurzen Ausblick.  
	- Video zur Vorlesung am 30.06.2021 - kommt noch
		



### Semesteraufgabe

Die als Semesteraufgabe zu entwickelnde Webanwendung sollte

1. ein Frontend besitzen (muss nicht mit einem JavaScript-Framework erstellt werden),
2. das Frontend sollte responsive sein,
3. ein Backend (damit Daten auf dem Server verwaltet werden können), 
4. eine Datenbank zur persistenten Speicherung von Daten (das kann auch SQLite oder ähnlich In-Apps-Datenbanken sein),
5. installierbar sein,
6. offline nutzbar sein,
7. die IndexedDB verwenden,
8. Hintergrundsynchronisation verwenden,
9. Push-Nachrichten verwenden,
10. die Gelocation API verwenden,
11. die Kamera oder eine andere technische Schnittstelle (z.B. Sensoren, Mikrofon) verwenden.

Von den Punkten 5.-11. sollten 5 implementiert sein. Bitte erstellen Sie eine aussagekräftige README-Datei. Die erstellte Anwendung soll präsentiert werden und in einem kurzen Gespräch (15-20min) wird die Implementierung besprochen. 

Diese Liste wird noch um Hinweise zur Bewertung angepasst. 

---

