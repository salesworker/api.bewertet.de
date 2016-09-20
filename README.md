# bewertet.de API

## Schema

Die API kann sowohl über HTTP als auch über HTTPS angesprochen werden. Der Endpoint für alle Requests ist:

`www.bewertet.de/api`

Alle Anfragen an die API sollten dem folgenden Schema folgen:

`(http|https)://www.bewertet.de/api/<resource_name>.<format>`

Wobei <resource_name> der Name einer der unten genannten Ressourcen ist und <format> entweder xml oder json ist.

## HTTP Methoden

Die API verwendet die HTTP Methode GET um Ressourcen anzufordern und POST um Ressourcen zu erstellen.

## Authentifizierung

Alle Anfragen an die API müssen mindestens die folgenden drei Parameter beinhalten:

* api_key - Der Ihrer Firma zugeordnete Key
* timestamp - Die UTC Zeit im UNIX Timestamp Format 
* signature - Die individuell erstellte Signatur

Jeder Request muss mit einer Signatur signiert werden. Diese Signatur setzt sich aus den folgenden drei Parametern zusammen:

* api_key - Der Ihrer Firma zugeordnete API Key
* timestamp - Die UTC Zeit im UNIX Timestamp Format 
* api_secret - Das Ihrer Firma zugeordnete API Secret

Diese drei Strings müssen konkateniert werden. Der MD5 Hash dieses Strings bildet die Signatur.

### Beispiel

Sie möchten ein neues Token erstellen, hierfür muss ein POST Request an die folgende URL gesendet werden: 

`POST https://www.bewertet.de/api/invitation_token.json`

Folgende Parameter seien gegeben:

* `api_key=2VnR9sbAbTPY5cypmayc`
* `timestamp=1332755556986` 
* `secret=WM633BuRqfgzqtnPACpo`

Der konkatenierte String lautet also: 

`2VnR9sbAbTPY5cypmayc1332755963WM633BuRqfgzqtnPACpo`

Der MD5 Hash dieses Strings bildet die Signatur:

`75b0ad72a6a0a36ea551a57ccec3d3ac`

Die Anfrage sieht also wie folgt aus:

`POST http://www.bewertet.de/api/invitation_token.json?api_key=2VnR9sbAbTPY5cypmayc&timestamp=1332755556986 /`
`&signature=75b0ad72a6a0a36ea551a57ccec3d3ac`

Die erfolgreiche Antwort sieht folgendermaßen aus:

`[{"token":"aLdYsJ"}]`

## Ressourcen und Methoden

### Erstellung eines Einladungs-Token

`POST http://www.bewertet.de/api/invitation_token.json`

Optional kann der Parameter `count` übergeben werden. Diese Parameter bestimmt die Anzahl an Tokens, die erstellt werden soll. Der default Wert beträgt 1. Es können bis zu 30 Token gleichzeitig erstellt werden.

Der Einladungs-Link, der an den Nutzer weitergegeben kann, sieht folgendermaßen aus:

`https://www.bewertet.de/rating/new?invite_token=<token_ID>`

### Abfrage der aktiven Einladungs-Token

`GET http://www.bewertet.de/api/invitation_token.json`

Liefert eine Liste der aktuell gültigen Einladungs-Token zurück.
 
## Zugangsdaten

Falls Sie Zugang zu unserer API erhalten möchten, wenden Sie sich bitte an info@bewertet.de oder rufen Sie uns an unter 0221-677797-0.
