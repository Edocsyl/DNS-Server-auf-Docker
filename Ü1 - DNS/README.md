
# Übung 1 - Testumgebung: DNS Server & Host's auf Docker

Dieses Projekt stellt ein DNS Server mit zwei Host zur Verfügung. Auf den Hosts können Abfragen an den DNS Server gestellt werden.

Infrasturkutr (Docker Container):
  ```
  +------+     +------- +     +------+
  | Host |     | DNS    |     | Host |
  |  1   | --> | Server | <-- |  2   |
  +------+     +--------+     +------+
  ```

Ablauf des Aufbaus der Testumgebung: 
1. Image erstellen
2. DNS-Server Container erstellen & DNS Server starten
3. 2x Host erstellen & *nslookup* Abfragen stellen

> Wichtig: Das Netzwerk *teko-net* wird vorausgesetzt.

Inspiriert durch @foo0x29a

## Docker Image

Zur Vorbereitung wird das Image *dns_teko_image* ab dem Dockerfile erstellt. Diese beinhaltet den DNS Deamon *bind9* und *dnsutils* um DNS Abfragen zu erstellen. Weiter benötigen wir ein Netzwerk *teko-net* in welchem die Infrasturkur operiert.

### Docker Image "dns_teko_image" ab Dockerfile erstellen

    > docker build -t dns_teko_image .

## Container

### DNS-Server
Mit diesem Command wird ein Containter *dns-server* erstellt.

    > docker run -d --rm --name=dns-server \
    --net=teko-net --ip=172.20.0.2 --dns=172.20.0.2 \
    -e "type=dns" \
    dns_teko_image

### Run DNS Server

    > docker exec -d dns-server /etc/init.d/bind9 start

### Zusätzliche Commands

#### Stop DNS Server

    > docker exec -d dns-server /etc/init.d/bind9 stop

#### Container auflisten

    > docker container list

## Hosts 1&2

### Host 1 erstellen
    > docker run -d --rm --name=host-1 \
    --net=teko-net --ip=172.20.0.3 --dns=172.20.0.2 \
    dns_teko_image

### Host 2 erstellen
    > docker run -d --rm --name=host-2 \
    --net=teko-net --ip=172.20.0.4 --dns=172.20.0.2 \
    dns_teko_image
