# IndexedDB 

Wir haben jetzt verschiedene Ressourcen in statischen und dynamischen Caches gespeichert. Diese Ressourcen lagen als Dateien vor, die wir über eine URL abrufen konnten, also `*.html`-, `*.js`-, `*.css`- Dateien und Bilder. Jetzt wollen wir dynamisch *Daten* speichern, sogenannten *dynamischen Inhalt*. Diese Daten können ausgelesen und den unterschiedlichen Dateien hinzugefügt bzw. durch Dateien hinzugefügt werden. Wir können uns das wirklich wie eine Datenbank vorstellen, aus der wir diese Daten ziehen, nur dass diese Datenbank nicht extern in einem Datenbankmanagementsystem verwaltet wird, sondern durch den Browser. Wir haben unter den Developer Tools diese "Datenbank" vielleicht schon im `Application`-Reiter auf der linken Seite unter `Storage` entdeckt. Es handelt sich um die `IndexedDB`. 

Bei der `IndexedDB` handelt es sich um eine *transaktionsbasierte* Datenbank, die Schlüssel-Werte-Paare im Browser speichert. *Transaktionsbasiert* bedeutet dabei, dass ganze *Transaktionen* ausgeführt werden, die aus einzelnen Aktionen bestehen können. Wenn nur eine Aktion einer Transaktion fehlschlägt, dann wird keine der Aktionen dieser Transaktion ausgeführt. Das bedeutet, eine *Transaktion*  wird entweder ganz oder gar nicht ausgeführt. Unsere Transaktionen bestehen aber typischerweise nur aus wenigen Aktionen, das Transaktionskonzept spielt deshalb keine große Rolle. 

Wir können beliebige Daten in die `IndexedDB` speichern, also auch Bilder, Dateien, Arrays, Objekte, usw. Ein wichtiger Unterschied zum `Lokal Storage` ist, dass wir sowohl über den "normalen" JavaScript-Thread unserer Webanwendung als auch über den Service Worker auf die `IndexedDB` zugreifen können. 

### Das idb-Paket

Da die API zur `IndexedDB` sehr umständlich zu handhaben ist und viele *Callbacks* erfordert, wird die Verwendung anderer Pakete empfohlen, die sich als *Wrapper* um die API legen und die Verwendung von Promises ermöglichen. Oft wird z.B. [Dexie](https://dexie.org/) verwendet. Wir verwenden zunächst den [idb-Warpper](https://github.com/jakearchibald/idb) von Jake Archibald. Sie können dieses Paket per

```bash
npm install idb
```

installieren oder von der [GitHub](https://github.com/jakearchibald/idb)-Seite downloaden. Ich habe die `npm install idb`-Variante gewählt. Nach der Installation des Paketes erstellen wir eine Datei `db.js` im `public/src/js`-Ordner und geben dort schonmal ein (aus der `README.md` von `idb`): 

=== "public/src/js/db.js"
    ```js
    import { openDB, deleteDB, wrap, unwrap } from 'idb';

    async function doDatabaseStuff() {
      const db = await openDB(…);
    }
    ```

Im Service Worker haben wir normalerweise keinen direkten Zugriff auf die Skripte und Dateien unserer Webanwendung. Dafür gibt es jedoch die `importScripts()`-Anweisung. Wir importieren damit unsere `db.js`-Datei in den Service Worker und wir laden diese Datei auch in den Cache:

=== "public/sw.js"
    ```js linenums="1" hl_lines="1 18"
    importScripts('/src/js/db.js');

    const CURRENT_STATIC_CACHE = 'static-v3';
    const CURRENT_DYNAMIC_CACHE = 'dynamic-v3';

    self.addEventListener('install', event => {
        console.log('service worker --> installing ...', event);
        event.waitUntil(
            caches.open(CURRENT_STATIC_CACHE)
            .then(cache => {
                console.log('Service-Worker-Cache erzeugt und offen');
                cache.addAll([
                    '/',
                    '/index.html',
                    '/src/js/app.js',
                    '/src/js/feed.js',
                    '/src/js/material.min.js',
                    '/src/js/db.js',
                    '/src/css/app.css',
                    '/src/css/feed.css',
                    '/src/images/htw.jpg',
                    'https://fonts.googleapis.com/css?family=Roboto:400,700',
                    'https://fonts.googleapis.com/icon?family=Material+Icons',
                    'https://code.getmdl.io/1.3.0/material.blue_grey-red.min.css'
                ]);
            })
        );
    })

    self.addEventListener('activate', event => {
        console.log('service worker --> activating ...', event);
        event.waitUntil(
            caches.keys()
            .then(keyList => {
                return Promise.all(keyList.map(key => {
                    if (key !== CURRENT_STATIC_CACHE && key !== CURRENT_DYNAMIC_CACHE) {
                        console.log('service worker --> old cache removed :', key);
                        return caches.delete(key);
                    }
                }))
            })
        );
        return self.clients.claim();
    })

    self.addEventListener('fetch', event => {
        // check if request is made by chrome extensions or web page
        // if request is made for web page url must contains http.
        if (!(event.request.url.indexOf('http') === 0)) return; // skip the request. if request is not made with http protocol

        event.respondWith(
            caches.match(event.request)
            .then(response => {
                if (response) {
                    return response;
                } else {
                    return fetch(event.request)
                        .then(res => { // nicht erneut response nehmen, haben wir schon
                            return caches.open(CURRENT_DYNAMIC_CACHE) // neuer, weiterer Cache namens dynamic
                                .then(cache => {
                                    cache.put(event.request.url, res.clone());
                                    return res;
                                })
                        });
                }
            })
        );
    })
    ```

