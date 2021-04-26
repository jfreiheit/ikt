# Übungen


##### Übung 1 (Grundgerüst)

??? "Übung 1"

	1. In der ersten Übung geht es "nur" darum, das [Grundgerüst](../grundgeruest/#grundgerust-unserer-pwa) zu verstehen. Arbeiten Sie dazu diesen Abschnitt durch. Sie werden feststellen, dass sich die meisten Anweisungen (insb. im `HTML`-Code) auf [Material Design Lite](https://getmdl.io/) beziehen. 
	2. Um zu erkennen, was einen [Material Design Lite](https://getmdl.io/)-Bezug hat (und somit nicht wirklich wichtig ist),  ändern Sie das Grundgerüst so, dass Sie nicht [Material Design Lite](https://getmdl.io/), sondern [Bootstrap](https://getbootstrap.com/docs/4.6/getting-started/introduction/) verwenden. Werfen Sie also Material Design Lite komplett raus und ersetzen es vollständig durch Bootstrap. Löschen Sie die `material.min.js` aus dem `public/js`-Ordner.
	3. Starten Sie am besten damit, diese drei Zeilen aus den beiden `index.html`-Dateien zu löschen:
		```html
		<link href="https://fonts.googleapis.com/css?family=Roboto:400,700" rel="stylesheet">
		<link rel="stylesheet" href="https://fonts.googleapis.com/icon?family=Material+Icons">
		<link rel="stylesheet" href="https://code.getmdl.io/1.3.0/material.blue_grey-red.min.css">
		```
	4. Fügen Sie stattdessen den CSS-Link und das JS-Bundle aus [https://getbootstrap.com/docs/4.6/getting-started/introduction/](https://getbootstrap.com/docs/4.6/getting-started/introduction/) ein. 
	5. Sie können ja versuchen, dass es möglichst ähnlich aussieht:
		![uebung1](./files/51_uebung1.png)


##### Übung 2 (Web App Manifest)

??? "Übung 2"

	1. Erweitern Sie Ihre Anwendung (oder das Grundgerüst) um ein Web App Manifest. Verwenden Sie zur Erstellung des Manifestes am besten den [Web-App-Manifest-Generator](https://www.dunplab.it/web-app-manifest-generator). 
	2. Wählen Sie ein eigenes Icon. Beachten Sie, dass das Original-Icon die Maße 512x512 Pixel aufweisen muss. Der [Web-App-Manifest-Generator](https://www.dunplab.it/web-app-manifest-generator) fügt das Original-Icon nicht dem Manifest hinzu. [Lighthouse](../tools/#lighthouse) beschwert sich darüber, dass dem Manifest ein 512x512-Icon fehlt. Fügen Sie dieses am besten noch händisch hinzu. 
	3. Die Anwendung soll in dem Moment installiert werden, wenn die Nutzerin das erste Mal auf den `+`-Button klickt. Das heißt, es wird das `beforeinstallprompt`-Ereignis ausgelöst und die Behandlung dieses Ereignisses sorgt dafür, dass Sie die Anwendung genau dann installieren, wenn Sie das erste Mal den `+`-Button klicken. ![addbutton](./files/52_uebung2.png)
	4. Hinweise und Hilfestellungen finden Sie z.B. [hier](https://web.dev/codelab-make-installable/) oder im [Skript](../manifest/#das-beforeinstallprompt-ereignis) (enthält weitere Links) oder im [Video zum Manifest](http://../#woche-2-manifest).

