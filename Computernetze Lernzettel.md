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
### Um Kollisionen zu vermeiden kam die Idee des Token Ring auf. Hier wird ein Token von Host zu Host gereicht. Das erspart Kollisionen. Solange sie sich nicht gegenseitig überholen, ist es problemlos möglich, mehrere Token im Kreis laufen zu lassen und damit den Durchsatz zu erhöhen.

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

## **FTP**
## FTP Protokoll:
### FTP ist ein Protokoll, was für die Datenübertragung  über ein Netzwerk von einem Computer zum anderen verwendet wird.

### FTP ist sitzungsgebunden, zwischen Client und Server wird eine dauerhafte Verbindung aufgebaut. Innerhalb  einer Sitzung können mehrere Befehle ausgeführt werden ohne dass jedes Mal eine neue Verbindung hergestellt werden muss.

### Das FTP-Protokoll benutzt eine Authentifizierung, dabei wird das Passwort im Klartext übertragen.

### FTP verwendet wellKnown Ports. 21 für den Austausch von Befehlen und Port 20 für Datei Übertragung.

## FTP Aktiv- und Passivmodus
### Bei der Übertragung der Daten kann kann FTP mit **aktiven** oder **passiven** Modus betrieben werden.

## Aktiv:
- Der Client sendet über seinen einen Befehl an den Port 21 des Servers
- Der Server bestätigt den Befehl mit einem Statuscode über Port 21 Client
- Kurz danach sendet der Server Daten über Port 20 auf den Port des Clients
- Der Client sendet dann die Bestätigung an den Server und bricht die Kontrollverbindung ab
### Das Problem ist, dass der Server unaufgefordert Daten an den Client Sendet, dadurch können Probleme mit der NAT entstehen. Sobald die NAT eine Datei bekommt, schaut diese in einer Tabelle nach, welche IP-Adresse den Auftrag gegeben hat und schickt das Ergebnis. Bei einer unaufgeforderten Datenübertragung, weiß die NAT nicht wer der Auftraggeber ist und verwirft das Paket.

## Passiv:
- Der Client sendet seinen Befehl an an den Port 21 des Servers
- Der Server sagt dem Client das er die Pakete über einen zufälligen Port wie 1234 sendet
- Der Client öffnet eine Verbindung zum Port 1234
- Der Server sendet daten über einen eigenen Port die Pakete an Port 1234 des Clients
-  Der Server schließt die Datenverbindung und der Client die Kontrollverbindung
### Alle Verbindungen werden vom Client initiiert, weil weil ausgehende Verbindungen normalerweise erlaubt sind, und es keine eingehenden Verbindungen gibt, die blockiert werden müssten.
---
## **NAT**

### IP-Adressen sind Mangelware, die Lösung ist innerhalb eines LANs private IP-Adressen zu verwenden, die dann hinter einem Router mit NAT verborgen liegen.
### Dadurch muss der Provider nur eine internetfähige IP-Adresse vergeben, die für die dahinterliegenden Hosts ins Internet geht, indem sie ihre Anfragen durch den Router erledigen lassen.

## _Umsetzung:_
### Will der Client ins Internet, werden seine Pakete automatisch an einen NAT fähigen Router gesendet
- der Router merkt sich in einer Tabelle die lokale IP-Adresse des Clients und dessen Port, sowie die IP-Adresse und den Port der Zieladresse
- Der Router sendet das Paket unter seiner Internet-IP-Adresse und eigenem Port
- Der angesprochene Server schickt seine Antwort an die IP und Port des Routers
- Der Router schaut in seiner Tabelle, welche Client IP und Port Kombination hinter dem Paket stecken, die er über den Port sendet
- Der Router ersetzt die Adresse des Clients durch seine eigene im Paket und leitet sie weiter ins Lokale Netzwerk
### Aus Sicht des Clients ist nicht erkennbar, dass sich der Router zwischengeschaltet hat.

### Eine NAT ist eine sehr wirksame Schranke gegen Attacken aus dem Internet.
---
# Mail

## SMPT:
### Beschreibt das Senden der Mails an einen Mail-Server, der ständig zur Verfügung steht. Dieser kann die Mails entweder an einen anderen Mail-Server weitersenden oder, falls er der Zielserver ist, die Mails an seine User verteilen.

### Im Ursprung sendet das Protokoll alle seine Nachrichten im Klartext und  und es war keine Authentifizierung vorhergesehen. Heutzutage werden die Übertragung verschlüsselt aber nicht die Nachricht selber, die bleibt im Postfach Unverschlüsselt.

### Aus Sicherheitsgründen erlaubt SMPT das Versenden an Nachrichten nur, wenn Sender oder Empfänger der Domain des Servers angehören.

### SMPT ist nicht statuslos, obwohl es ohne Anmeldung funktioniert. Das Protokoll ist textbasiert, als Daten werden nur druckbare Zeichen verwendet, somit können keine binären Daten übertragen werden.
---
# SMPT Absender:
## Mail From:
### muss eine korrekte E-Mail-Adresse enthalten und wird geprüft.

## From:
### muss keine korrekte E-Mail-Adresse enthalten. Er wird aber dem Empfänger angezeigt.
---
# SMPT Mail Inhalt
### SMTP definiert das Ende einer Mail-Nachricht mit einem Punkt in einer Leerzeile.

### Deutsche Umlaute im Nachrichtentext können nicht direkt übertragen werden, sondern müssen umkodiert werden.
---
# Client Befehle
- HELO: startet Verbindung
- EHLO: startet die Verbindung nach dem Extended SMTP
- DATA: Damit wird die eigentliche Nachricht eingeleitet
- QUIT: Ende der Verbindung
- VRFY: lasse die E-Mail-Adresse bestätigen

# Server Antwort
- 1xx: Die Anforderung ist akzeptiert, aber noch nicht verarbeitet. Bestätigung erforderlich
- 2xx: Die Anforderung wurde erfolgreich ausgeführt
- 3xx: Die Anforderung ist verstanden, benötigt aber weitere Informationen
- 4xx: Temporärer Fehler und könnte bei Wiederholung glücken
- 5xx: Fataler Fehler
---
# POP3
### POP3 ist für das herunterladen von Mails vom Server auf einen lokalen Client. Standardmäßig werden die E-Mails **vom Server gelöscht**, sobald sie heruntergeladen wurden. POP3 ist optimiert auf möglichst kurze Onlineverbindungen, weil nach Verbindungsdauer bezahlt wird. POP3 erzwingt eine Anmeldung mit Benutzer und Passwort.
---
# IMAP

### IMAP ist das Protokoll für die Verwaltung von E-Mails auf einem Mailserver. DAs Protokoll erzwingt eine Anmeldung  und kann Nachrichten auf den Server löschen. Da Benutzer mehrere Geräte haben, ist IMAP darauf optimiert, dass mehrere Clients die Mails bearbeiten können. 
---
# MIME
### Beim versenden von JPG-Fotos bzw. Binären Daten muss MIME verwendet werden. Dabei werden die Bilder in Base64 kodiert, dadurch werden die um ein drittel größer.
---
#  Vertrauliche Nachrichten per SMTP
### Wenn Sie SMTP-Server ohne Authentifizierung ins Internet stellen, riskieren Sie, dass Ihre Domain auf die Spamlist kommt.

### Sofern Sie Ihre Mails nicht explizit vor dem Versenden verschlüsseln, liegen sie auf dem Server des Providers im Klartext vor.
### Verschlüsselte Mails werden per MIME übertragen
---
# DNS
### Der DNS Server muss dem Client Form einer IP-Adresse bekannt gegeben werden, weil Clients nur über IP-Adresse mit anderen kommunizieren können.

## Kanonischer Name:
### Ein kanonischer Name  bezeichnet den eindeutigen, primären Namen der zu einer IP-Adresse gehört. Dieser wird vom DNS zurückgegeben, wenn die IP-Adresse zum Namen aufgelöst wird.





