# Übung 2 - OpenLDAP 


## *openldap* Installation & Konfiguration
Um die 

### Volumes erstellen
    > docker volume create ldap_database
    > docker volume create ldap_config


### openldap Container erstellen

    > docker run -p 389:389 --name ldap-service \
    --hostname ldap-service \
    --env LDAP_ORGANISATION="Teko" \
    --env LDAP_DOMAIN="teko.local" \
    --env LDAP_ADMIN_PASSWORD="adminPassword" \
    --env LDAP_BASE_DN="dc=teko,dc=local" \
    --volume ldap_database:/var/lib/ldap \
    --volume ldap_config:/etc/ldap/slapd.d \
    --detach osixia/openldap:1.4.0


### *phpLDAPadmin* Contianer erstellen
asdasd

    > docker run -p 6443:443 --name phpldapadmin-service \
    --hostname phpldapadmin-service \
    --link ldap-service:ldap-host \
    --env PHPLDAPADMIN_LDAP_HOSTS=ldap-service \
    --detach osixia/phpldapadmin:0.9.0


    --env PHPLDAPADMIN_HTTPS=false \




Username (DN): cn=admin,dc=teko,dc=local
Password: adminPassword