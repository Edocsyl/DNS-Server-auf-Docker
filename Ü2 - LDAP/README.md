# Übung 2 - OpenLDAP 
In dieser Übung wird ein OpenLDAP Container *ldap-service* erstellt. Mit dem weitern Container *phpldapadmin-service* kann per Webinterface *phpldapadmin* auf den LDAP Server zugegriffen werden. 

## *openldap* und *phpLDAPadmin* Container Installation & Konfiguration

### Volumes erstellen

Um die Daten *openldap* Daten persistent auf dem Docker-Host zu speichern, werden die foglenden zwei Volumes erstellt.

    > docker volume create ldap_database
    > docker volume create ldap_config

### openldap Container erstellen
Der OpenLDAP Container basiert auf einem Docker-Image von osixia.

    > docker run -p 389:389 --name ldap-service \
    --hostname ldap-service --net=teko-net --ip=172.20.0.10 \
    --env LDAP_ORGANISATION="Teko" \
    --env LDAP_DOMAIN="teko.local" \
    --env LDAP_ADMIN_PASSWORD="adminPassword" \
    --env LDAP_BASE_DN="dc=teko,dc=local" \
    --volume ldap_database:/var/lib/ldap \
    --volume ldap_config:/etc/ldap/slapd.d \
    --detach osixia/openldap:1.4.0


### phpLDAPadmin Contianer erstellen
Dieser Container enthält ein Webserver mit [phpLDAPadmin](http://phpldapadmin.sourceforge.net/wiki/index.php/Main_Page). Dies ist ein Web basierten LDAP-Client mit welchem auf den *ldap-service* zugegriffen wird. 

    > docker run -p 6443:443 --name phpldapadmin-service \
    --hostname phpldapadmin-service --net=teko-net --ip=172.20.0.11 \
    --env PHPLDAPADMIN_LDAP_HOSTS=ldap-service \
    --detach osixia/phpldapadmin:0.9.0

Über die URL https://localhost:6443, wird der LDAP Client aufgeruffen. Nach bestätigen des selbst signierten Zertifikats, werden die folgenden Logindaten zum einloggen benötigt:  

- Username (DN): cn=admin,dc=teko,dc=local
- Password: adminPassword
