# REST-Server

```bash
mkdir backend
cd backend
npm init
```

`package.json` wird erzeugt. Sie können ales mit `Enter` bestätigen oder eigene Eingaben wählen. 

#### Express

Dann noch `express` installieren:

```bash
npm install --save express
```

`package.json` sieht dann vielleicht so ähnlich aus (eventuell müssen Sie noch `"type": "module",` händisch hinzufügen[^1]):

[^1]:  

```json
{
    "name": "backend",
    "version": "1.0.0",
    "description": "Einfaches Backend für IKT-PWA",
    "main": "server.js",
    "type": "module",
    "scripts": {
        "test": "echo \"Error: no test specified\" && exit 1"
    },
    "keywords": [
        "IKT",
        "PWA",
        "REST"
    ],
    "author": "J. Freiheit",
    "license": "ISC",
    "dependencies": {
        "express": "^4.17.1"
    }
}
```

#### nodemon

Wir installieren noch [nodemon](https://www.npmjs.com/package/nodemon), damit wir nicht immer neu `node` aufrufen müssen. Nach Eingabe von 

```bash
npm install nodemon --save-dev
```

wurde die `package.json` um 

```json
,
"devDependencies": {
    "nodemon": "^2.0.7"
}
```

erweitert. Wir könnten nun noch in der `package.json` unter `"scripts"` z.B.

```json
   "scripts": {
        "watch": "nodemon ./server.js",
        "test": "echo \"Error: no test specified\" && exit 1"
    },
```

hinzufügen und können die Anwendung dann über `npm run watch` starten. 


#### server.js

Im Ordner `backend` eine `server.js` erzeugen mit 

```js
import express from 'express';

const app = express();
const port = 3000;

app.get('/', (req, res) => {
    res.send(`just testing ...`);
});

app.listen(port, () => console.log(`Server listening on port ${ port } ...`));
```

`npm run watch` startet `nodemon`, welches `node server.js` startet. Auf der Konsole erscheint 

```bash
[nodemon] restarting due to changes...
[nodemon] starting `node ./server.js`
Server listening on port 3000 ...
```

und im Browser unter `localhost:3000` erscheint `just testing ...`.

#### cors

Mit `express` haben wir einen *HTTP Server* erstellt. Wir benötigen noch das `cors`-Modul, um *cross-origin resource sharing* möglich zu machen. 

```bash
npm install --save cors
```

Dort, wo früher, der `body-parser` verwendet wurde, ist seit Express-Version 4.16 nun direkt die Verwendung von `express` möglich. `body-parser` ist wohl nun sogar `deprecated`. 

Wir ergänzen `server.js` um

```js linenums="1" hl_lines="2 7-9"
import express from 'express';
import cors from 'cors';

const app = express();
const port = 3000;

app.use(cors());
app.use(express.urlencoded({ extended: false }));
app.use(express.json());

app.get('/', (req, res) => {
    res.send(`just testing ...`);
});

app.listen(port, () => console.log(`Server listening on port ${ port } ...`));
```

### mysql

```bash
npm install --save mysql
```


