
# DNS Server mit Host auf Docker

Dieses Projekt stellt in DNS Server mit zwei Host zur Verfügung. Auf den Hosts können Abfragen an den DNS Server gestellt werden.

> Wichtig: Das Projekt ist möglicherweise nicht vollständig Dokumentiert

## Docker Image & Netzwerk

Zur Vorbereitung wird das Image *dns_teko_image* ab dem Dockerfile erstellt. Diese beinhaltet den DNS Deamon *bind9* und *dnsutils* um DNS Abfragen zu erstellen. Weiter benötigen wir ein Netzwerk *teko-net* in welchem die Infrasturkur operiert.

    host-1 --> DNS-Server <-- host-2

### Docker Image "dns_teko_image" ab Dockerfile erstellen

> docker build -t dns_teko_image .

### Netzwerk Erstellen

> docker network create teko-net --subnet 172.20.0.0/24

### Zusätzliche Commands

#### Netzwerk löschen

> docker network remove teko-net

#### Netzwerke auflisten

> docker network list

## Container

### DNS-Server

> docker run -d --rm --name=dns-server --net=teko-net --ip=172.20.0.2 --dns=172.20.0.2 -e "type=dns" dns_teko_image

### Run DNS Server

> docker exec -d dns-server /etc/init.d/bind9 start

### Zusätzliche Commands

#### Stop DNS Server

> docker exec -d dns-server /etc/init.d/bind9 stop

#### Container auflisten

docker container list

## Hosts 1&2

> docker run -d --rm --name=host-1 --net=teko-net --ip=172.20.0.3 --dns=172.20.0.2 dns_teko_image

> docker run -d --rm --name=host-2 --net=teko-net --ip=172.20.0.4 --dns=172.20.0.2 dns_teko_image

## Testing
