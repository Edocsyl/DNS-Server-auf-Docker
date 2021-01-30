# Teko Informationssysteme
In diesem Repository werden die Übungen, welche im Fach "Informationssysteme" bearbeitet werden, dokumentiert. 

> Info: Die Übungen sind möglicherweise nicht vollständig dokumentiert oder enthalten Fehler. Durch ein "Pull Request" kannst du Ergänzungen am Projekt vornehmen. 

## *teko-net* Netzwerk
Die Übungen werden im Docker Netzwerk *teko-net* betrieben. Dieses Netzwerk wird für alle Übungen vorausgesetzt. 
### Netzwerk Erstellen

    > docker network create teko-net --subnet 172.20.0.0/24

### Zusätzliche Commands

#### Netzwerk löschen

    > docker network remove teko-net

#### Netzwerke auflisten

    > docker network list

#### Netzwerk vollständig anzeigen
    > docker network inspect teko-net


## Übung 1 - Testumgebung: DNS Server & Host's auf Docker
In dieser Übung wird eine "DNS Testumgebung" mit dem *bind9* per Docker aufgesetzt. 

## Übung 2 - OpenLDAP Server & Administrationskonsole
In dieser Übung wird ein OpenLDAP Server basieren auf dem Image von [@osixia](https://github.com/osixia) aufgesetzt.
