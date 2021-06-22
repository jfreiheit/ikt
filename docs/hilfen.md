# Hilfen

Hier erläutern wir in losem Zusammenhang einzelne Aspekte. 


### Arrow-Funktionen

*Arrow-Funktionen* werden auch als *Lambda-Ausdrücke* bezeichnet. Eine Arrow-Funktion ist eine Kurzschreibweise für eine anonyme Funktion. Anstelle von `function()` schreibt man nur noch einen  Pfeil. Enthält die anonyme Funktion sogar nur ein Argument (Parameter), kann man links vom Pfeil sogar die runden Klammern weglassen. Auch die geschweiften Klammern des Funktionskörpers können entfallen. Wenn die geschweiften Klammwern weggelassen werden, dann entspricht die rechte Seite des Pfeils dem Rückgabewert der Funktion, d.h. es kann sogar `return` weggelassen werden. Folgende Funktionsdefinitionen sind äquivalent:

``` javascript
function(foo) = {return foo+1;}
(foo) => {return foo+1;}
foo => {return foo+1;}
foo => foo+1;
```

### Callback-Funktionen

Eine *Callback*-Funktion ist eine Funktion, die einer anderen Funktion als Parameter übergeben wird. Callback-Funktionen sind z.B. [hier](https://developer.mozilla.org/en-US/docs/Glossary/Callback_function) erläutert. Darin finden Sie auch das folgende einfache Beispiel einer Callback-Funktion:

``` javascript linenums="1"
function greeting(name) {
  alert('Hello ' + name);
}

function processUserInput(callback) {
  var name = prompt('Please enter your name.');
  callback(name);
}

processUserInput(greeting);
```

In den Zeilen 1-3 wird eine Funktion `greeting()` definiert, welche einen `name` erwartet. Diese Funktion gibt `Hello ` zusammen mit dem Namen in einem Alarmfenster aus. Die Funktion `greeting()` wird als *Callback*-Funktion in der Funktion `processUserInput()` (Zeilen 5-8) verwendet. Das heißt, die Funktion `greeting()` wird der Funktion `processUserInput()` als Parameter übergeben. Innerhalb der Funktion `processUserInput()` heißt die Referenz auf die Funktion `greeting()` `callback`. Der Parametername kann beliebig gewählt werden. Wir die Funktion `processUserInput()` aufgerufen (Zeile 10) und die Funktion `greeting()` als Parameter übergeben, dann erscheint zunächst ein Eingabefenster, in dem der Name eingeben wird und dieser Name wird der `greeting()`-Funktion als Parameter übergeben. Es erscheint das Alarmfenster mit der Ausgabe `Hello ` plus dem Namen. Der Funktion `processUserInput()` könnte auch jede andere Funktion als Callback-Funktion übergeben werden. 


### JSON Web Tokens (JWT)

Mithilfe von [JSON Web Tokens (JWT)](https://jwt.io/introduction) verwalten wir den Zugriff auf Webseiten (oder auf andere Server). Ein JSON Web Token besteht aus drei Teilen:

- einem *Header*, der den Typ des Tokens enthält (`JWT`) und den Verschlüsselungsalgorithmus, der zur Verschlüsselung der Informationen verwendet wird, z.B. [`SHA256`](https://de.wikipedia.org/wiki/SHA-2).  
- einem *Paload*, der die Informationen über die Ntzerin enthält und eventuell weitere Informationen, wie z.B. Rolle der Nutzerin, z.B. `admin`
- einer *Signatur*, die mithilfe des angegebenen Verschlüsselungsalgorithmus die Inforationen des Headers und der Payload verschlüsselt. Mithilfe der Signatur kann überprüft werden, ob ide Informationen im Header oder im Payload geändert wurden oder nicht. 

Die drei Teile werden jeweils durch einen Punkt getrennt, d.h. ein JWT hat die Form `header.payload.signature`. 

Mithilfe des [Codierers/De-Codierers](https://jwt.io/#debugger-io) von JWT können Sie das Codieren bzw. Decodieren nachvollziehen. Angenommen, Ihr *Header* ist 

```jason
{
  "alg": "HS256",
  "typ": "JWT"
}
```

, d.h. Sie verwenden `SHA256` zur Verschlüsselung und der Typ ist `JWT`. Dann ist der erste Teil des JWT

```json
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9
```

Angenommen, Ihr *Payload* ist 

```jason
{
  "data": [
    {
      "id": 1,
      "username": "test",
      "email": "test@test.de",
      "password": "098f6bcd4621d373cade4e832627b4f6"
    }
  ],
  "iat": 1609061622
}
``` 

Die `data` haben hier eine Struktur, wie sie häufig für Login-Daten verwendet werden. Das Passwort `test` ist `md5`-verschlüsselt. `iat` steht für *issued at*  und gibt die Zeit ([Unix-Time](https://www.unixtimestamp.com/index.php)) an, zu der das JWT erzeugt wurde (hier 27.12.2020). Dann ist der zweite Teil des JWT

```json
eyJkYXRhIjpbeyJpZCI6MSwidXNlcm5hbWUiOiJ0ZXN0IiwiZW1haWwiOiJ0ZXN0QHRlc3QuZGUiLCJwYXNzd29yZCI6IjA5OGY2YmNkNDYyMWQzNzNjYWRlNGU4MzI2MjdiNGY2In1dLCJpYXQiOjE2MDkwNjE2MjJ9
```

Wenn Sie als "sichere" Passphrase `secret` wählen und damit die *Signatur* erstellen, dann ist der dritet Teil des JWT

```json
XBWOvX8OceGmx8u77YfsyQtupYYO9p9mUurvIqqwgdk
```

Ausführliche Informationen über JWT finden Sie [hier](https://jwt.io).
