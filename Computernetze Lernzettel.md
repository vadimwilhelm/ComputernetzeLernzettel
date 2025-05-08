## **Netzwerkkommunikation in Paketen**

### Kommunikationsströme werden auf Pakete verteilt und nacheinander an das Ziel gesandt und dort wieder zusammengesetzt. Nur auf der Basis von Paketen ist es möglich, dass mehrere Hosts in einem Netzwerk parallel miteinander kommunizieren können.
---

## **Schichtmodelle

| **Ebene** | **Schicht**        | **Protokolle**                 |
| --------- | ------------------ | ------------------------------ |
| 1         | Netzzugangsschicht | Ethernet, WLAN, ATM, FDDI, ... |
| 2         | Internetschicht    | IPv4 bzw. IPv6, ICMP, IPsec    |
| 3         | Transportschicht   | TCP, UDP                       |
| 4         | Anwendungsschicht  | HTTP, SMTP, DNS                |

---
## **Netzwerk-Topologie**

### Beschreibt eine physische oder logische Anordnung und Verbindung zwischen den Hots.
1. Bus
2. Ring
3. Stern

## Bus
### An einen Bus werden mehrere Hosts angeschlossen, die alle Pakete hören können und auch über ihn Pakete versenden können. Damit teilen sie die angeschlossenen Hosts die Bandbreite. Vor allem kann das parallele Senden zu Kollisionen führen.

### Diese Kollisionen reduzieren die Bandbreite noch einmal nutzlos, so dass man versucht, diese Kollisionen zu erkennen und zu vermeiden.


- Vorteile:
	- Einfache Verlegung
	- niedrige Kosten
	- passiv, benötigt also keine Eigenintelligenz

- Nachteile:
	- Hohes Kollisionsrisiko
	- alle beteiligten Hosts teilen sich die Bandbreite
	- Durchtrennung eines Kabels führt zu einem Teilausfall des gesamten Netzwerks

## Ring
### Um Kollisionen zu vermeiden kam die Idee des [Token Ring](https://willemer.de/informatik/net/nethard.htm#token) auf. Hier wird ein Token von Host zu Host gereicht. Das erspart Kollisionen. Solange sie sich nicht gegenseitig überholen, ist es problemlos möglich, mehrere Token im Kreis laufen zu lassen und damit den Durchsatz zu erhöhen.

- Vorteile:
	- Kollisionsfrei
	- Nachteile:
	- Hohe Kosten, großer Aufwand
	- Durchtrennung eines Kabels führt zu einem Totalausfall des gesamten Netzwerks.

## Stern

### Bei der Stern-Topologie steht in der Mitte des Netzwerks ein Vermittler, meist ein Switch. Alle Hosts des Netzwerks sind mit diesem verbunden. Wollen zwei Hosts miteinander kommunizieren, werden deren Leitungen miteinander verbunden.

### Der Switch führt eine Tabelle aller Geräte-MAC-Adressen, die an einem Abgang angeschlossen ist. So kann er schnell die gewünschte Verbindung herstellen.

### Auf diese Weise werden die Kollisionen reduziert und die Bandbreite erhöht, weil mehrere Kommunikationspaare parallel die maximale Bandbreite des Netzwerks nutzen können.

- Vorteile:
	- Weitestgehend kollisionsfrei
	- Durchtrennung eines Kabels führt nur zum Ausfall eines Hosts.

- Nachteile:

	- Switch benötigt Eigenintelligenz
	- Ausfall des Switches führt zum Totalausfall des Netzwerks
---
# **HTTP**
### http ist ein Protokoll der Anwenderschicht des TCP/IP

### http ist statuslos. Das bedeutet, dass die Sitzung nach der Antwort durch den Server beendet wird. Dabei wird jede Anfrage von Client zum Server unabhängig von anderen Anfragen bearbeitet. Hat der Server auf die Anfrage geantwortet wird die verbind getrennt und der Server merkt sich die Sitzung nicht.


### _http-Befehle:_
## Der User kann folgende Befehle an den Server schicken:
- GET: Holt eine Datei vom Server
- HEAD: holt nur den Head-Anteil, also die Information über die Seite
- POST: Sendet eine Formularinhalt an den Server
- PUT: wird zum hochladen von Datei verwendet
- DELETE: Zum Löschen einer Server-Ressource

### _HTTP-Status-Codes:_
### Der Server antwortet auf Anfragen mit einem Statuscode:
- 1xx: Informationen
- 2xx: Erfolgreich
- 3xx: Es sind weitere Aktionen erforderlich
- 4xx: Client-Fehler
- 5xx: Server-Fehler
---
## **Cookie**
### http ist statuslos, leider ist es beim Online Shoppen nicht hilfreich. Der Server sendet kleine Dateipakete, beim Betreten der Webseite, dem Client.

### Dies geschieht über das HTTP-Header-Feld Set-Cookie.

### Cookies enthalten die URL der ausstellenden Website. Ruft der Client(Browser) die Website erneut auf, sendet er den Cookie automatisch mit. In dem Cookie ist meist eine eindeutige Sitzungsnummer oder Kennung gespeichert, damit der Server weiß, wem die Sitzung gehört und sendet dann die entsprechenden Informationen an den Client.

### Cookies haben ein Ablaufdatum und sind an einer Domain gebunden.

### Probleme ergeben sich, wenn Cookies an Server weitergegeben werden, die gar nicht der Shop-URL entsprechen, weil dieser Server dann nachvollziehen kann, welchen Shop der Client besucht hat.
---

## **FTP/NAT**
## FTP Protokoll:
### FTP ist ein Protokoll, was für die Datenübertragung  über ein Netzwerk von einem Computer zum anderen verwendet wird.

### FTP ist sitzungsgebunden, zwischen Client und Server wird eine dauerhafte Verbindung aufgebaut. Innerhalb  einer Sitzung können mehrere Befehle ausgeführt werden ohne dass jedes Mal eine neue Verbindung hergestellt werden muss.

### Das FTP-Protokoll benutzt eine Authentifizierung, dabei wird das Passwort im Klartext übertragen.

### FTP verwendet wellKnown Ports. 21 für den Austausch von Befehlen und Port 20 für Datei Übertragung.

## FTP Aktiv- und Passivmodus
### Bei der Übertragung der Daten kann kann FTP mit *aktiven** oder **passiven** Modus betrieben werden.

## Aktiv:
- Der Client sendet über seinen einen Befehl an den Port 21 des Servers
- Der Server bestätigt den Befehl mit einem Statuscode über Port 21 Client
- Kurz danach sendet der Server Daten über Port 20 auf den Port des Clients
- Der Client sendet dann die Bestätigung an den Server und bricht die Kontrollverbindung ab
### Das Problem ist, dass der Server unaufgefordert Daten an den Client Sendet, dadurch können Probleme mit der NAT entstehen.



---
