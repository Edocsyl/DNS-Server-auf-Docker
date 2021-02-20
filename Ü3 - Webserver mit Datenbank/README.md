# Übung 3 - Webserver mit Datenbank 

In dieser Übung wird ein Nginx Webserver Container *web-service*, ein Container *php-service* und ein Containter *mysql-service* erstellt.

Infrasturkutr (Docker Container):
  ```
 +-------------+  +-------------+
 | NGINX       |  | PHP         |
 | web-service |  | php-service |
 +-------------+  +-------------+
                          ↕
                 +---------------+
                 | MYSQL         |
                 | mysql-service |
                 +---------------+
  ```

## Aufsetzen der Infrastruktur
Compose ist ein Werkzeug zur Definition und Ausführung von Multi-Container-Docker-Anwendungen. 

> Hinweis: Falls das Netzwerk 'teko-net' nicht existiert, bitte das Kapitel [Netzwerk erstellen](https://github.com/Edocsyl/Teko-Informationssysteme#netzwerk-erstellen) beachten.

### Ordnerstruktur erstellen
Die Beispielscripts werden persistent auf den lokalen Host gespeichert und über ein Volume in den Container gemappt. Im Verzeichnis *C:\Temp\root\www* sind diese Scripts abgelegt. Im Ordner *C:\Temp\root\database* liegen die Daten der Datenbank. Diese Ordnerstruktur muss vorgängig erstellt werden. 

    > mkdir C:\Temp\root
    > mkdir C:\Temp\root\www
    > mkdir C:\Temp\root\database

Nach dem erstellen der Ordnerstruktur, werden die Scripts in das WWW Verzeichnis kopiert. 

### Mit der Application Docker-Compose wird das Projekt *u3_webserver-datenbank* gestartet

Die drei Container werden in der *docker-compose.yml* beschrieben

    > docker-compose -p u3_webserver-datenbank up

Nachdem die Container aufgesetzt sind, kann über die URL https://localhost:8081, den NGINX Webserver aufgerufen werden. 

> Hinweis: In der *site.conf* wird der NGINX Server konfiguriert. Um den Inhalt des *www* Verzeichnis aufzulisten, wurde die Konfiguration *autoindex on;* gesetzt. Dies wird in einer Produktiven Umgebung nicht empfohlen. 
