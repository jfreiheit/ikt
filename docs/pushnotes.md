# Push Notifications

*Push Notifications* sind sinnvoll, um die Nutzerin einer App über Neuigkeiten zu informieren, sogar dann, wenn die Anwendung (und der Browser!) geschlossen ist (sind). Mit *Push Notifications* können Nutzerinnen wieder "zurück an die App geholt" werden, d.h. mithilfe von *Push Notifications* kann man dafür sorgen, dass Nutzerinnen die App wieder öffnen, um sich die Neuigkeiten genauer anzuschauen. Die Neuigkeiten können neue Tweets, E-Mails, Nachrichten, Anrufe usw. sein. 

Das Prinzip, das für die Push-Benachrichtungen umgesetzt wird, sieht auf den ersten Blick etwas kompliziert aus:

![push](./files/73_push.png)

Im Zentrum stehen zunächst die Webanwendung und der Service Worker. Die Webanwendung meldet sich bei den Push-Benachrichtigungen an und der Service Worker verwaltet diese. Jeder Browser hat eine eigenen "eingebauten" *Push Server*. Eine *Push-Anmeldung* (*Push Subscription*) erlaubt den Zugriff auf einen *Push-API-Endpunkt* auf den Push-Server. Die eigentliche *Push-Benachrichtigung* kommt jedoch vom eigenen Server. Er sendet die Push-Nachricht an den *In-Browser Push Server*, dieser löst damit ein `push`-Ereignis beim Service Worker aus und der Service Worker schickt die *Push-benachrichtigung* an die Webanwendung. 

Wir schauen uns alle diese Schritte im Detail an.

