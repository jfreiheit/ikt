# Hintergrundsynchronisation

Hintergrundsynchronisation erlaubt die Synchronisation von daten, selbst dann, wenn die Anwendung offline ist. Diese "Synchronisation" erfolgt natürlich "asynchron". Angenommen, Sie geben offline Daten in die Anwendung ein und wollen diese versenden, z.B. an das Backend, dann wird dieser Request so lange in Ihrer Anwendung gespeichert, bis Sie wieder online sind und erst dann ausgeführt. 

Das Situation ist die Folgende:

![backgroundsync](./files/69_background.png)

Es sollen Daten an das Backend gesendet werden, aber die Internetverbindung ist unterbrochen. Deshalb werden die Daten in die IndexedDB gespeichert und im Service Worker wird eine *Sync Task* registriert. 

![backgroundsync](./files/70_background.png)

Sobald die Verbindung wieder steht, wird ein *Sync*-Event im Service Worker ausgelöst und dieser sendet die Daten an das Backend (`POST-Request`).

Dadurch, dass der Service Worker diesen `POST-Request` ausführt (und die Daten dabei mitsendet), kann die Hintergrundsynchronisation sogar dann stattfinden, wenn die Webanwendung bereits geschlossen ist! Deshalb sollten wir einfach immer beim Senden von Daten eine *Sync Task* registrieren, weil es sein kann, dass die Daten noch gar nicht vollständig gesendet wurden, bevor wir den Browsertab schließen. 

### Zunächst ein bisschen mehr responsive

Unser *HTW Insta* entwickelt sich langsam. Deshalb ist hier vielleicht ein guter Zeitpunkt, um die Anwendung noch etwas mehr *responsive* zu gestalten. 

#### Media Queries

Zum Beispiel sind die `Cards` stets in fester Größe, unabhängig davon, ob wir die Anwendung am Desktop betrachten oder am Mobilgerät. 

Dazu können wir in unsere `feed.css` ein paar *Media queries* einfügen:

=== "/src/css/feed.css"
	```css
	#create-post {
	    z-index: 1001;
	    position: fixed;
	    width: 100%;
	    min-height: 100vh;
	    overflow-y: scroll;
	    bottom: 0;
	    top: 56px;
	    background: white;
	    text-align: center;
	    visibility: hidden;
	}

	.main-image {
	    max-width: 100%;
	    margin: auto;
	    display: block;
	}

	.whiteText {
	    color: white;
	}

	.floating-button {
	    z-index: 1000;
	    position: fixed;
	    bottom: 0;
	    right: 0;
	    padding: 30px;
	}

	.input-section {
	    display: block;
	    margin: 10px auto;
	}

	.shared-moment-card.mdl-card {
	    margin: 10px auto;
	    width: 80%;
	}

	@media (min-width: 600px) {
	    .shared-moment-card.mdl-card {
	        width: 60%;
	    }
	}

	@media (min-width: 1200px) {
	    .shared-moment-card.mdl-card {
	        width: 45%;
	    }
	}

	.shared-moment-card .mdl-card__title {
	    height: 250px;
	}

	@media (min-height: 600px) {
	    .shared-moment-card .mdl-card__title {
	        height: 300px;
	    }
	}

	@media (min-height: 1200px) {
	    .shared-moment-card .mdl-card__title {
	        height: 380px;
	    }
	}		
	```

Wir haben sowohl für die Viewport-Höhe als auch für die Viewport-Breite zwei *Breakpoints* eingebaut. Bei jeweils `600px` bzw. `1200px` ändern sich die Angaben zur Höhe bzw. Breite der Bilder in den `Cards`. **Achtung:** In `feed.js` muss dazu die Zeile 

```
cardTitle.style.height = '180px';
```

gelöscht werden! Die Höhe und Breite der Bilder in den `Cards` passt sich jetzt (besser)  der Viewport-Breite und -Höhe an. Bei den Breiten haben wir sogar %-Angaben verwendet (gut), bei den Höhen nur feste Pixel-Werte (nicht so gut). Sie können gerne damit herumspielen und es an Ihre Bedürfnisse anpassen. Mehr zu Media Queries finden Sie z.B. [hier](https://www.w3schools.com/css/css_rwd_mediaqueries.asp) und [hier]()https://wiki.selfhtml.org/wiki/CSS/Media_Queries.


#### srcset-Attribut für img

Die Verwendung der Bilder können wir noch auf eine andere Art *responsive* gestalten. Je nach Viewport-Größe können die Bilder eingebunden werden, deren Auflösung "ausreicht". In dem `/public/src/images/`-Ordner haben wir für unser Hauptbild oben drei verschiedene Versionen:

- `htw.jpg`, mit der Auflösung `898 x 343` Pixel,
- `htw-lg.jpg`, mit der Auflösung `1199 x 457` Pixel und
- `htw-sm.jpg`, mit der Auflösung `480 x 183` Pixel.

Es wäre unsinnig, beisielsweise das `htw-lg.jp` auf einem schmalen Viewport anzuzeigen, da dafür die Auflösung des `htw-sm.lpg` völlig genügt. Da Letzteres auch noch deutlich kleiner ist (`43 KB`), als das `htw-lg.jpg`-Bild (`170 KB`), ließe sich auch die Ladezeit verringern, wenn für mobile Geräte das kleiner Bild verwendet würde. Auf der anderen Seite sieht dieses Bild aufgrund seiner niedrigen Auflösung in großen Viewports (also am Desktop-Monitor) nicht gut aus. Dort benötigen wir das `htw-lg.jpg`. Um diesen Wechsel der Bilder je nach Viewport-Größe zu vereinfachen, wurde in HTML5 für das `img`-Element das Attribut `srcset` hinzugefügt (siehe z.B. [hier](https://developer.mozilla.org/en-US/docs/Learn/HTML/Multimedia_and_embedding/Responsive_images)  oder [hier](https://html.com/attributes/img-srcset/)). In unserer `index.html` können wir also das Einbinden des `img`-Elementes wie folgt erweitern:


=== "/index.html"
	```html linenums="88"
	<img srcset="/src/images/htw-lg.jpg 1200w, 
                 /src/images/htw.jpg 900w,
                 /src/images/htw-sm.jpg 480w" 
         src="/src/images/htw.jpg" alt="HTW Wilhelminenhof" class="main-image">
	```

Zuvor stand dort einfach nur: `<img src="/src/images/htw.jpg" alt="HTW Wilhelminenhof" class="main-image">`. Wir haben also das `srcset`-Attribut hinzugefügt. Das generelle Template dafür sieht so aus:

```html
<img srcset="url size, 
			 url size,
			 url size" 
	 src="default url" >
```

Das heißt, nach den URLs auf die jeweiligen Bilder schreiben wir noch die Größe des Viewports, ab denen die Bilder verwendet werden sollen, also `1200w, 900w, 480w`. Dabei steht `w` für `width`. Möglich wäre auch noch, dass man statt `w` ein `x` angibt und dann die Anzahl der Pixel verwendet für die Viewportgröße. Das Laden der unterschiedlichen Images kann in den DeveloperTools unter `Network` beobachtet werden. 


#### Animationen

Wenn wir auf der Hauptseite auf den `+`-Button klicken, dann "erscheint" das Formular zur Dateneingabe einfach. Das liegt daran, dass wir in der `feed.js` bei den Funktionen `openCreatePostModal()` und `closeCreatePostModal()` die Sichtbarkeit einfach an- und ausschalten. Wir könnten das aber auch etwas "netter" durch eine Animation gestalten. Dazu verwenden wir [translateY](https://developer.mozilla.org/de/docs/Web/CSS/transform-function/translateY()) und [transition](https://developer.mozilla.org/de/docs/Web/CSS/transition). `translateY()` verschiebt ein Element in `y`-Richtung (also rauf oder runter) und `transition` kann eine Zeit übergeben werden, die angibt, wie lange der Wechsel von Werten einer Eigenschaft dauern soll - also eine Animation. 

In der `feed.ccs` ändern wir für die `id=create-post`:

```css linenums="1" hl_lines="11 13-14"
#create-post {
    z-index: 1001;
    position: fixed;
    width: 100%;
    min-height: 100vh;
    overflow-y: scroll;
    bottom: 0;
    top: 56px;
    background: white;
    text-align: center;
    /* visibility: hidden; */

    transform: translateY(100vH);
    transition: transform 0.3s;
}
```

Die Zeile `11` kann natürlich ganz raus. In der `feed.js` ändern wir für die beiden Methoden:

```js linenums="1" hl_lines="2 6"
function openCreatePostModal() {
    createPostArea.style.transform = 'translateY(0)';
}

function closeCreatePostModal() {
    createPostArea.style.transform = 'translateY(100vH)';
}
```

und danach "slided" das Formular von unten nach oben ein. `vH` ist eine Einheit in Relation zum Viewport. `100vH` ist die gesamte Viewporthöhe, `1vH` ist der 100te Teil der Viewporthöhe (siehe z.B. [hier](https://wiki.selfhtml.org/wiki/CSS/Wertetypen/Zahlen,_Ma%C3%9Fe_und_Ma%C3%9Feinheiten)).

### Daten senden

In unserer *HTW Insta*-Anwendung sorgen wir nun zunächst dafür, dass wir auch Daten eingeben und diese versenden können. Ausgangspunkt ist dieser [Stand des Projektes](./files/IKT-PWA-05.zip) (noch ohne die responsiven Erweiterungen).

Wir wollen dazu den `Speichern`-Button aus der `index.html` 

```html linenums="76"
<button class="mdl-button mdl-js-button mdl-button--raised mdl-button--colored mdl-color--accent"
        type="submit" id="post-btn">Speichern
</button>
```

mit der `feed.js` verbinden. Dazu definieren wir uns zunächst mithilfe von jQuery weitere Variablen für den direkten Zugriff auf Stuerelemente. Wir erweiteren die `feed.js` um die hervorgehobenen Zeilen:

=== "/src/js/feed.js" 
	```js linenums="1" hl_lines="5-7"
	let shareImageButton = document.querySelector('#share-image-button');
	let createPostArea = document.querySelector('#create-post');
	let closeCreatePostModalButton = document.querySelector('#close-create-post-modal-btn');
	let sharedMomentsArea = document.querySelector('#shared-moments');
	let form = document.querySelector('form');
	let titleInput = document.querySelector('#title');
	let locationInput = document.querySelector('#location');
	```

Nun können wir einfacher auf das `submit`-Ereignis des `Speichern`-Buttons reagieren. Wir melden dazu das Formular an den Ereignislistener für das `submit`-Ereignis in der `feed.js` an:


=== "/src/js/feed.js" 
	```js linenums="79"
	form.addEventListener('submit', event => {
	    event.preventDefault(); // nicht absenden und neu laden

	    if (titleInput.value.trim() === '' || locationInput.value.trim() === '') {
	        alert('Bitte Titel und Location angeben!')
	        return;
	    }

	    closeCreatePostModal();
	});
	```

Wir verhindern zunächst das Standardverhalten beim `submit`-Ereignis, nämlich das Absenden der Daten und das Neuladen der Seite (Zeile `80`). In Zeile `82` prüfen wir, ob beide `input`-Elemente, also sowohl für `title`, als auch für `location` einen Wert enthalten. Die JavaScript-`trim()`-Funktionen entfernt "Leerzeichen" aller Art am Ende des Strings (auch Tabs, Zeilenumbrüche etc.). Sollte eines der beiden (oder beide) Eingabefelder leer sein, beenden wir die Funktion mit einem `alert` und bleiben in dem Formular. `alert` ist natürlich nicht so toll, ein `toast` wäre viel besser, aber wir haben in unserer `index.html` nur einen `toast` für das erfolgreiche Speichern vordefiniert. Wenn beide Eingabefelder befüllt sind, wird das Formularfenster verlassen. Wir erweitern diese Funktion nun um die Registrierung an die *Sync Task*. 

#### Sync-Task registrieren

Wenn wir das Formular absenden und die in dem Formular eingegebenen Daten speichern wollen, steuern wir dies nun über eine *Sync Task*. Diese *Sync Task* sorgt dafür, dass die Daten (irgendwann) tatsächlich gespeichert werden, auch wenn wir gerade offline sind oder während des Speicherns offline geschaltet werden. Für eine solche *Sync Task* existiert die [SyncManager-API](https://developer.mozilla.org/en-US/docs/Web/API/SyncManager). Wenn Sie auf diesen Link klicken, dann sehen Sie, dass die `SyncManager-API`

1. nur 2 Methoden besitzt, nämlich `register()` und `getTags()` und 
2. dass sie bis jetzt leider nur von Chrome und Edge unterstützt wird. Allerdings auch in allen Android-Geräten (mit Chrome oder WebView) und somit trotzdem eine große Reichweite besitzt. 

Wir erweitern die Anmeldung an den Listener für das `submit`-Event zunächst wie folgt:


=== "/src/js/feed.js" 
	```js linenums="79" hl_lines="11-16"
	form.addEventListener('submit', event => {
	    event.preventDefault(); // nicht absenden und neu laden

	    if (titleInput.value.trim() === '' || locationInput.value.trim() === '') {
	        alert('Bitte Titel und Location angeben!')
	        return;
	    }

	    closeCreatePostModal();

	    if('serviceWorker' in navigator && 'SyncManager' in window) {
	        navigator.serviceWorker.ready
	            .then( sw => {
	                sw.sync.register('sync-new-post');
	            });
	    }
	});
	```

In diesem kleinen Code-Stückchen sind einige Dinge beachtenswert. Erstens, wird die `SyncManager-API` vom Service Worker verwendet, aber wir sind hier ja in `feed.js`, also in der Webanwendung. Wir können die Registrierung an die *Sync Task* nicht einfach in die `sw.js` schreiben, da das auslösende Ereignis der Registrierung (nämlich das Absenden des Formulars) in der Webanwendung stattfindet und wir dieses Ereignis in `feed.js` behandeln. Wir benötigen in `feed.js` also einen Zugriff auf den Service Worker. 

Dazu fragen wir zunächst, ob der Service Worker überhaupt durch den Browser unterstützt wird und auch, ob die `SyncManager-API` durch den Browser unterstützt wird. Dies geschieht in Zeile `89`. Dort fällt auf, dass der Service Worker eine Eigenschaft von `navigator` ist, die `SyncManager-API` eine Eigenschaft von `window`. [Window](https://developer.mozilla.org/de/docs/Web/API/Window) ist das Fenster, das ein DOM Dokument (also eine Webanwendung) enthält. Eine Eigenschaft von `window` ist `navigator` (also `window.navigator`). Das [Navigator](https://developer.mozilla.org/de/docs/Web/API/Window/navigator)-Objekt liefert Informationen über den Browser, in dem die Anwendung ausgeführt wird. 

Die (`readonly`)-Eigenschaft `ready` eines Service Workers ist eine Promise, welche `resolved` ist, sobald der Service Worker `active` ist. Siehe [hier für `ready`](https://developer.mozilla.org/en-US/docs/Web/API/ServiceWorkerContainer/ready). Über diese Promise erlangen wir Zugriff auf den Service Worker in unserer Webanwendung. Die [sync](https://developer.mozilla.org/en-US/docs/Web/API/ServiceWorkerRegistration/sync)-Eigenschaft ist in dem Interface [ServiceWorkerRegistration](https://developer.mozilla.org/en-US/docs/Web/API/ServiceWorkerRegistration) definiert. Die `register()`-Funktion ist eine der beiden Methoden aus der `SyncManager-API` und registriert eine *Sync Task*. Jeder *Sync Task* wird ein `tag` zugewiesen (ähnlich einer `id`). über diesen `tag` kann später auf diese *Sync Task* zugegriffen werden. Wir haben dieser *Sync Task* den `tag` `'sync-new-post'` gegeben. 

Die *Sync Task* ist nun registriert. Allerdings weiß der Service Worker noch gar nicht, was er bei dieser *Sync Task* überhaupt synchronisieren soll. Das definieren wir jetzt.

#### Daten in die IndexedDB speichern

Die Daten, die (später) synchronisert werden sollen, werden zunächst in der IndexedDB gespeichert. Dort können Sie so lange bleiben, bis die Webanwendung (wieder) online ist, um dann an das Backend durch den Service Worker gesendet zu werden. Dazu erzeugen wir uns ein passendes JavaScript-Objekt `post`:


=== "/src/js/feed.js" 
	```js linenums="79" hl_lines="14-18"
	form.addEventListener('submit', event => {
	    event.preventDefault(); // nicht absenden und neu laden

	    if (titleInput.value.trim() === '' || locationInput.value.trim() === '') {
	        alert('Bitte Titel und Location angeben!')
	        return;
	    }

	    closeCreatePostModal();

	    if('serviceWorker' in navigator && 'SyncManager' in window) {
	        navigator.serviceWorker.ready
	            .then( sw => {
	            	let post = {
	            		id: new Date().toISOString(),
	            		title: titleInput.value,
	            		location: locationInput.value,
	            	};
	                sw.sync.register('sync-new-post');
	            });
	    }
	});
	```

Die `id` wurde hinzugefügt, um einen eindeutigen Identifier für den `post` in der IndexedDB zu haben (`keyPath`). Damit der Wert auch eindeutig ist, wird der Zeitstempel zum String umgewandelt und verwendet (Zeile `93`). 

Diesen `post` wollen wir nun in die IndexedDB speichern. Dazu steht uns aus der `db.js` die Funktion `writeData()` zur Verfügung. Diese Funktion erwartet als ersten Parameter den `Store`, in dem wir den `post` speichern wollen. Derzeit haben wir einen `Store` in unserer IndexedDB definiert, den `Store` `posts`:


=== "/src/js/db.js" 
	```js linenums="1" hl_lines="5"

	const db = idb.openDB('posts-store', 1, {
	    upgrade(db) {
	        // Create a store of objects
	        const store = db.createObjectStore('posts', {
	            // The 'id' property of the object will be the key.
	            keyPath: 'id',
	            // If it isn't explicitly set, create a value by auto incrementing.
	            autoIncrement: true,
	        });
	        // Create an index on the 'id' property of the objects.
	        store.createIndex('id', 'id');
	    },
	});
	```

Diesen `Store` verwenden wir aber, um unsere Daten aus der Datenbank/dem Backend zu *cachen*. Wir verwenden ihn zum Schreiben und Lesen der Daten aus unserer Datenbank. Für das Synchroniseren der neuen Daten benötigen wir deshalb einen weiteren `Store`. Dazu kopieren wir einfach die `Store`-Erstellung in der `db.js` und nennen den neuhinzugekommen `Store` `sync-posts`:


=== "/src/js/db.js" 
	```js linenums="1" hl_lines="7-9"

	const db = idb.openDB('posts-store', 1, {
	    upgrade(db) {
	        db.createObjectStore('posts', {
	            keyPath: 'id',
	        }).createIndex('id', 'id');

	        db.createObjectStore('sync-posts', {
	            keyPath: 'id',
	        }).createIndex('id', 'id');
	    },
	});
	```

Gleichzeitig habe ich auch noch ein bisschen den Code gekürzt. Die Kommentare sind raus und das `autoIncrement: true` ist auch Standard, deshalb muss es nicht mit angegeben werden. Wenn wir die Anwendung nun ausführen, sehen wir unter `IndexedDB`, dass ein weiterer `Store` hinzugekommen ist:

![backgroundsync](./files/71_background.png)


Diesen Store verwenden wir nun, um die neuen `post`-Daten in die IndexedDB zu schreiben:

=== "/src/js/feed.js" 
	```js linenums="79" hl_lines="19-22"
	form.addEventListener('submit', event => {
	    event.preventDefault(); // nicht absenden und neu laden

	    if (titleInput.value.trim() === '' || locationInput.value.trim() === '') {
	        alert('Bitte Titel und Location angeben!')
	        return;
	    }

	    closeCreatePostModal();

	    if('serviceWorker' in navigator && 'SyncManager' in window) {
	        navigator.serviceWorker.ready
	            .then( sw => {
	            	let post = {
	            		id: new Date().toISOString(),
	            		title: titleInput.value,
	            		location: locationInput.value,
	            	};
	                writeData('sync-posts', post)
	                    .then( () => {
	                        sw.sync.register('sync-new-post');
	                    });
	            });
	    }
	});
	```

Die Registrierung der *Sync Task* ist nur dann sinnvoll, wenn die Daten auch tatsächlich in der IndexedDB gespeichert wurden. Deshalb erfolgt die Registrierung in dem `resolved`-Pfad der `writeData`-Promise. 

Jetzt können wir noch unseren `toast` verwenden, den wir in der `index.html` definiert haben. Hierbei handelt es sich um eine *Material Design Lite*-Komponente [Snackbar](https://getmdl.io/components/#snackbar-section):

=== "/index.html"
	```html linenums="98"
    <div id="confirmation-toast" aria-live="assertive" aria-atomic="true" aria-relevant="text" class="mdl-snackbar mdl-js-snackbar">
        <div class="mdl-snackbar__text"></div>
        <button type="button" class="mdl-snackbar__action"></button>
    </div>
	```


In der `feed.js` verketten wir die Promise für das Schreiben der Daten in die IndexedDB weiter und bestätigen dies mit einer Snackbar-Nachricht:


=== "/src/js/feed.js" 
	```js linenums="79" hl_lines="21 23-27"
	form.addEventListener('submit', event => {
	    event.preventDefault(); // nicht absenden und neu laden

	    if (titleInput.value.trim() === '' || locationInput.value.trim() === '') {
	        alert('Bitte Titel und Location angeben!')
	        return;
	    }

	    closeCreatePostModal();

	    if('serviceWorker' in navigator && 'SyncManager' in window) {
	        navigator.serviceWorker.ready
	            .then( sw => {
	            	let post = {
	            		id: new Date().toISOString(),
	            		title: titleInput.value,
	            		location: locationInput.value,
	            	};
	                writeData('sync-posts', post)
	                    .then( () => {
	                        return sw.sync.register('sync-new-post');
	                    })
	                    .then( () => {
	                        let snackbarContainer = new MaterialSnackbar(document.querySelector('#confirmation-toast'));
	                        let data = { message: 'Eingaben zum Synchronisieren gespeichert!', timeout: 2000};
	                        snackbarContainer.showSnackbar(data);
                    	});
	            });
	    }
	});
	```

Beachten Sie, dass Sie das `return` in Zeile `99` einfügen, damit die Promise verkettet werden kann. Nachdem Sie nun Daten in das Formular eingegeben und auf `Speichern` geklickt haben, erscheint für 2 Sekunden unten eine Bestätigungsnachricht:


![backgroundsync](./files/72_background.png)


#### Ein Fallback

Wir haben festgelegt, was passieren soll, wenn der Browser *Service Worker* und die *SyncManager-API* unterstützt. Wir sollten jedoch ein *Fallback* einbauen für den Fall, dass das nicht der Fall ist. Viel bleibt uns für diesen Fall nicht übrig, zu tun. Wir können nur versuchen, die Daten, die wir in das Formular eingegeben haben, sofort an das Backend zu senden. 

Daten an das Backend senden, können wir bereits. Wir nutzen dazu die `fetch()`-Funktion und verwenden die `POST`-Methode. Wir fügen dazu eine Funktion `sendDataToBackend()` in die `feed.js` ein und rufen diese im `else`-Fall für die Behandlung des `submit`-Ereignisses auf:


=== "/src/js/feed.js" 
	```js linenums="79" hl_lines="1-23 54-56"
	function sendDataToBackend() {
	    fetch('http://localhost:3000/posts', {
	        method: 'POST',
	        headers: {
	            'Content-Type': 'application/json',
	            'Accept': 'application/json',
	        },
	        body: JSON.stringify({
	        	id: null,
	            title: titleInput.value,
	            location: locationInput.value,
	            image: '',
	            })
	    })
        .then( response => {
            console.log('Data sent to backend ...', response);
            return response.json();
        })
	    .then( data => {
	        console.log('data ...', data);
	        updateUI(Object.entries(data));
	    });
	}


	form.addEventListener('submit', event => {
	    event.preventDefault(); // nicht absenden und neu laden

	    if (titleInput.value.trim() === '' ||  locationInput.value.trim() === '') {
	        alert('Bitte Titel und Location angeben!')
	        return;
	    }

	    closeCreatePostModal();

	    if('serviceWorker' in navigator && 'SyncManager' in window) {
	        navigator.serviceWorker.ready
	            .then( sw => {
	                let post = {
	                    id: new Date().toISOString(),
	                    title: titleInput.value,
	                    location: locationInput.value,
	                };
	                writeData('sync-posts', post)
	                    .then( () => {
	                        return sw.sync.register('sync-new-post');
	                    })
	                    .then( () => {
	                        let snackbarContainer = new MaterialSnackbar(document.querySelector('#confirmation-toast'));
	                        let data = { message: 'Eingaben zum Synchronisieren gespeichert!', timeout: 8000};
	                        snackbarContainer.showSnackbar(data);
	                    });
	            });
	    } else {
	        sendDataToBackend();
	    }
	});
	```


So ganz toll ist die Fallback-Funktionalität nicht. Dazu müsste die `id` nicht mit einem festen Wert belegt werden und die `image`-Eigenschaft mit einem richtigen Bild. Es lässt sich aber einmal ausprobieren, indem man dafür sorgt, dass die Bedingung `if('serviceWorker' in navigator && 'SyncManager' in window)` `false` ist (z.B. `&& false`), aber es geht hier zunächst nur um das Prinzip und deshalb werden wir uns hier zunächst nicht weiter darum kümmern, dass dies vollständig fehlerfrei durchgeführt werden kann.  

Stattdessen kümmern wir uns nun darum, dass das `sync`-Ereignis im Service Worker behandelt wird. Das geschieht immer dann, wenn der Service Worker erkennt, dass die Internetverbindung wieder hergestllt wurde. 


#### Ereignisbehandlung des `sync`-Events

Wenn der Service Worker erkennt, dass die Verbindung zum Internet wieder hergestellt ist, wird automatisch das `sync`-Event ausgelöst. Dieses Ereignis wird auch dann ausgelöst, wenn die Internetverbindung besteht **und** eine *Sync Task* registriert wurde. Wir wollen in diesem Fall die Daten aus der IndexedDB an das Backend senden. Dazu erweitern wir die `sw.js` um die Behandlung des `sync`-Ereignisses. Wir fügen diese Ereignisbehandlung an das Ende der `sw.js` ein:


=== "sw.js" 
	```js linenums="104"
	self.addEventListener('sync', event => {
	    console.log('service worker --> background syncing ...', event);
	    if(event.tag === 'sync-new-post') {
	        console.log('service worker --> syncing new posts ...');
	        event.waitUntil(
	            readAllData('sync-posts')
	                .then( dataArray => {
	                    for(let data of dataArray) {
	                        console.log('data from IndexedDB', data);
	                        // diese Daten an das Backend senden (siehe Fallback)
	                    }
	                })
	        );
	    }
	})
	```

Wir fügen dem Service Worker also einen `EventListener` hinzu, wie wir das bereits von den anderen Ereignisbehandlungen im Service Worker kennen. Das `sync`-Ereignis gibt auch die `tags` zurück, unter denen *Sync Tasks* gespeichert wurden. In unserem Fall war der verwendete `tag` `sync-new-post`. Wir verwenden auch erneut `event.waitUntil()`, um sicherzustellen, dass die Ereignisbehandlung nicht eher verlassen wird, bis alle definierten Anweisungen darin vollständig abgearbeitet wurden. Als erstes greifen wir dann lesend auf die IndexedDB unter Verwendung der `readAllData()`-Methode aus der `db.js`.

Diese Methode gibt ein Array aller gespeicherten Datensätze in der IndexedDB im Store `sync-posts` zurück. Mit einer `for`-Schleife betrachten wir jeden einzelnen Datensatz. Wir "wissen", dass ein solcher Datensatz ein JavaScript-Objekt mit den Eigenschaften `id`, `title` und `location` ist. 

Wir erweitern diese Behandlung nun um den Code, den wir zuvor für das *Fallback* verwendet haben. Wir senden die Daten an das Backend. Dazu können wir uns den Code von der Fallback-Implementierung kopieren und anpassen:


=== "sw.js" 
	```js linenums="104" hl_lines="10-31"
	self.addEventListener('sync', event => {
	    console.log('service worker --> background syncing ...', event);
	    if(event.tag === 'sync-new-post') {
	        console.log('service worker --> syncing new posts ...');
	        event.waitUntil(
	            readAllData('sync-posts')
	                .then( dataArray => {
	                    for(let data of dataArray) {
	                        console.log('data from IndexedDB', data);
	                        fetch('http://localhost:3000/posts', {
	                            method: 'POST',
	                            headers: {
	                                'Content-Type': 'application/json',
	                                'Accept': 'application/json',
	                            },
	                            body: JSON.stringify({
	                                id: null,
	                                title: data.title,
	                                location: data.location,
	                                image: '',
	                            })
	                        })
	                        .then( response => {
	                            console.log('Data sent to backend ...', response);
	                            if(response.ok) {
	                                deleteOneData('sync-posts', data.id)
	                            }
	                        })
	                        .catch( err => {
	                            console.log('Error while sending data to backend ...', err);
	                        })
	                    }
	                })
	        );
	    }
	})
	```

Für die Daten, die an das Backend gesendet werden, wird nun, im gegensatz zum Fallback, auf `data` zugegriffen, da wir ja die Daten senden, die aus der IndexedDB ausgelesen werden. Wenn die Daten erfolgreich an das Backend übertragen worden sind (`response.ok` in Zeile `128`), dann werden diese Daten mithilfe der `deleteOneDate()`-Funktion (aus `db.js`) gelöscht, da sie in der IndexedDB nicht weiter benötigt werden. Der Store `sync-posts` ist ja "nur" dazu da, die Daten so lange zwischenzuspeichern, bis sie ins Backend (in die persistente Datenbank) gesendet sind. Sollte stattdessen ein Fehler auftreten, wird er mithilfe von `catch()` abgefangen und dort ausgegeben. 

Wenn wir nun neue Daten in das Formular eingeben und auf Speichern klicken, werden die Daten zum Backend gesendet (ohne einen Wert für die `image`-Eigenschaft - der Wert von `id` wird durch die Datenbank erstellt.)


Das Ausprobieren der späteren Hintergrundsynchronisation erfolgt am Sichersten dadurch, dass Sie den Rechner komplett vom WLAN trennen. Das Offline-Schalten des Service Workers genügt dazu häufig nicht (bzw. wird beim Online-Schalten dann manchmal kein `sync`-Ereignis ausgelöst).

1. Schalten Sie das WLAN an Ihrem Rechner aus. 
2. Geben Sie über das Formular der Anwendung neue Daten ein und drücken Sie auf den `Speichern`-Button. 
3. Schauen Sie in den Developer Tools unter `IndexedDB` in den Store `sync-posts`. Dort sollten die neuen Daten nun gespeichert sein. 
4. Schalten Sie das WLAN wieder ein. Auf der Konsole erscheint die `fetch`-Nachricht für `POST "http://localhost:3000/posts"`.
5. In der persistenten Datenbank stehen die neuen Daten. 
6. Nach einem Reload der Anwendung werden diese Daten aus der Datenbank über das Backend gelesen (ohne Bilder) und erscheinen als weitere `Cards`.


!!! success
	Wir haben die Hintergrundsynchronisation implementiert! Das Senden der Daten an das Backend erfolgt über das Registrieren einer *Sync Task* und dem (zwischen-)Speichern der zu sendenden Daten in der IndexedDB. Durch die Ereignisbehandlung des `sync`-Ereignisses werden diese Daten an das Backend (und darüber in die Datenbank) geschrieben. Das `sync`-Ereignis wird ausgelöst, wenn der Service Worker online und eine *Sync Task* registriert ist. Wir können nun Daten eingeben und speichern, egal, ob wir online oder offline sind. Die Anwendung kann sogar geschlossen sein und trotzdem synchronisiert der Service Worker. 
































