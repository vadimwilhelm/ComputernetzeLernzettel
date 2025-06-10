## **Netzwerkkommunikation in Paketen**

### Kommunikationsströme werden auf Pakete verteilt und nacheinander an das Ziel gesandt und dort wieder zusammengesetzt. Nur auf der Basis von Paketen ist es möglich, dass mehrere Hosts in einem Netzwerk parallel miteinander kommunizieren können.
---

## **Schichtmodelle

| **Ebene** | **Schicht**        | **Protokolle**                 |
| --------- | ------------------ | ------------------------------ |
| 1         | Netzwerkschicht| Ethernet, WLAN, ATM, FDDI, ... |
| 2         | Sicherungsschicht    | IPv4 bzw. IPv6, ICMP, IPsec    |
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
---
## Rekursiv:

### Bei einer rekursiven Namensauflösung werden Anfragen, die ein lokaler DNS-Server nicht beantworten kann an dessen übergeordneten Server weitergeleitet, bis der oberste gemeinsame Server gefunden ist. Von dort werden nun für die jeweilige Domain verantwortlichen Server aufgesucht, bis die IP-Adresse gefunden ist. Diese wird dann auf dem umgekehrten Weg zurückgereicht.

## Iterativ:
### Beim iterativen Ansatz leitet der angefragte DNS-Server die Anfrage nicht weiter, sondern informiert den Anfrager, welcher DNS-Server für die weitere Auflösung des Namens zuständig ist. Der Anfrager muss also mehrere Anfragen stellen, bis die IP-Adresse gefunden ist.


### Der Client kann den DNS auffordern, rekursiv oder iterativ vorzugehen. Iterativ entlastet die TLD-Server
---
# RR
### Ein RR wird als Antwort auf eine DNS-Anfrage vom Server an den Client gesandt. In dem RR befinden sich die Informationen des DNS für den Client.
### Wenn der Client eine DNS-Anfrage stellt (z. B. nach der IP-Adresse einer Website), dann enthält der RR in der DNS-Antwort die IP-Adresse und der Client weiß danach, wohin (an welche IP) er die eigentliche Anfrage schicken muss.
---
## Sicherheit

### DNS ist unverschlüsselt
### DNSSEC verwendet Zertifikate, damit die Autorisierung des Servers geprüft werden kann

### Eine Anmeldung mit Benutzer und Passwort ist bei DNS nicht möglich.
---
# Zertifikate
### Zertifikate basieren auf asymmetrische Schlüssel, diese enthalten den öffentlichen Schlüssel des Dienstanbieters, die offen angeboten werden. Das Zertifikat enthält die URL des Dienstanbieters wie Domain-Namen. 
- Der Server erstellt ein Zertifikat und leitet es der CA weiter. 
- Die CA signiert den öffentlichen Schlüssel des Server mit ihrem privaten Schlüssel. Der öffentliche Schlüssel der Ca ist für bei dem Browser aufgelistet.
- Ruft der Browser den Server auf, schickt der Server sein Zertifikat mit dem öffentlichen Schlüssel, der URL und der Signatur der CA.
- Der Browser prüft die digitale Signatur im Zertifikat mithilfe des öffentlichen Schlüssels der CA

---
# Transportschicht-Ports-TCP-UDP

### Die Transportschicht ermöglicht die Kommunikation zwischen Prozessen auf verschiedenen Geräten. Sie wird von der Anwendungsschicht beauftragt, Daten zu übertragen. Um Prozesse auf einem Computer eindeutig identifizieren zu können, verwendet die Transportschicht sogenannte Ports. Diese Ports dienen als Adressen für Absender und Empfänger und werden in die Transportpakete eingefügt. Server verwenden dabei häufig sogenannte "well-known Ports", damit sich Client-Prozesse gezielt mit den entsprechenden Diensten verbinden können.

## Socket
### Ein Socket ist eine Datenstruktur, die vom Programm zum Senden und Empfangen benötigt wird. Ein Socket besteht aus diesen vier Dingen:

1. **IP-Adresse des Rechners**
    
2. **Port-Nummer** (z. B. 80 für Webserver)
    
3. **Protokoll** (meist TCP oder UDP)
    
4. **Zustand** (z. B. verbunden, geschlossen usw.)

## TCP
### Dateien werden in Pakete gepackt und können beim übertragen vom Client zum Server oder umgekehrt verloren gehen, zerstört werden oder aufgrund von Umwegen in der falschen Reihenfolge eintreffen. 
### Damit sich der Programmieren nicht ständig darum kümmern muss die Pakete zu reparieren, verwendet man in der Transportschicht TCP. Das führt alle Reparaturen automatisch, dadurch kommt bei größeren Paketen zu Verzögerungen, was Zeit kostet. Damit es nicht zu einer Überlastung kommt, hat das Paket ein Feld was die Größe des Paketes dem Sender mitteilt.

### Bei TCP sagt die Sequenznummer wo der Datenblock beginnt, sie ist wichtig für die Reihenfolge.

### Der Handshake ist wichtig für eine zuverlässige und geordnete Verbindung.

## UDP
### TCP ist zuverlässig aber sehr langsam und in manchen fällen ist Geschwindigkeit wichtiger als Zuverlässigkeit. Zum Beispiel beim Streamen oder bei sehrt kleinen Verbindungsdaten, bei denen es sinnvoller ist das verlorene Paket nochmal anzufragen, statt es zu reparieren.
### Die Vorteile sind:

- Keine Verzögerung durch Verbindungsaufbau
- Kein Verbindungsstatus bei Sender oder Empfänger notwendig
- Kleiner Header
- Keine Überlastkontrolle

---
# IP
## Private IP
### Ein Host (z. B. ein Computer oder Drucker) befindet sich immer in einem bestimmten lokalen Netzwerk (LAN). Innerhalb dieses LANs wird ein anderer Host direkt über seine Hardware-Adresse, also die MAC-Adresse, angesprochen. Handelt es sich jedoch nicht um das gleiche LAN, wird ein Router benötigt, der Daten in das fremde Netzwerk weiterleitet.

Dabei hilft die **IP-Adresse**, die in zwei Teile gegliedert ist:

- Der erste Teil bezeichnet das **Netzwerk** (Netzwerkanteil),
- der zweite Teil identifiziert den Host innerhalb dieses Netzwerks
### Private IP-Adressen lassen sich in Subnetze unterteilen, z. B. 192.168.1.0/24 in kleinere Bereiche.
--- 
## ## IPv4 einfach erklärt

### 🧱 Aufbau einer IPv4-Adresse

Eine **IPv4-Adresse** besteht aus **4 Zahlen** (je 1 Byte = 8 Bit), zum Beispiel:  
`192.168.109.34`

Diese Darstellung nennt man **"dotted decimal"**, weil die Zahlen durch Punkte getrennt sind.

---

### 🔍 Was bedeuten die Zahlen in der IP-Adresse?

Jede IPv4-Adresse besteht aus zwei Teilen:

- **Netzwerkteil**: Sagt, zu welchem Netzwerk die Adresse gehört.
    
- **Hostteil**: Sagt, welches Gerät im Netzwerk gemeint ist.
    

Wie viele Bit für das Netzwerk bzw. den Host verwendet werden, zeigt man durch eine **Subnetzmaske** oder die **CIDR-Notation**.

### 📏 CIDR-Notation (z. B. `/24`)

Die **CIDR-Notation** schreibt man mit einem Schrägstrich hinter der IP-Adresse:  
Beispiel: `192.168.109.34/24`

Das bedeutet:

- **Die ersten 24 Bit** gehören zum **Netzwerk**
    
- **Die letzten 8 Bit** gehören zum **Host**
    

In diesem Fall:

- Netzwerk: `192.168.109`
    
- Host: `34` → das einzelne Gerät im Netzwerk
    
### Subnetzmaske

Statt `/24` kann man auch eine sogenannte **Subnetzmaske** angeben.  
Diese besteht ebenfalls aus 4 Zahlen, z. B.: `255.255.255.0`

In binärer Form bedeutet das:

- Die Einsen stehen für den **Netzwerkteil**
    
- Die Nullen stehen für den **Hostteil**
    

Beispiel:

- `/24` = `255.255.255.0` = **24 Einsen und 8 Nullen**
    

### Die Subnetzmaske bestimmt also, wie eine IP-Adresse aufgeteilt wird – in Netzwerkadresse und Hostadresse.

---
# IPv6
### Die Darstellung einer IPv6-Adresse ist hexadezimal. Die Ziffern sind jeweils vierstellig (16 Bit) geordnet, getrennt durch einen Doppelpunkt.

### Früher wurde oft die MAC-Adresse eines Geräts in die IPv6-Adresse eingebaut, mithilfe der sogenannten EUI-64-Methode.

### Mac-Adresse: 00:1A:2B:3C:4D:5E
### IPv6: fe80::021a:2bff:fe3c:4d5e


### IPv6 kann durch ein IPv4-Netz transportiert werden, wenn IPv6 nicht direkt unterstützt wird.
###  Dabei wird das IPv6-Paket in ein IPv4-Paket eingekapselt und über das IPv4-Netz verschickt.
---

# Routing

