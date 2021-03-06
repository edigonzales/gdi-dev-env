# gdi-dev-env

## init.gradle
init-Datei für GRETL, um DB-Verbindungen und Abhängigkeiten den lokalen Gegebenheiten anzupassen.

## soconfig-DB
```
sudo -u postgres psql -d postgres -c 'ALTER USER ddluser WITH SUPERUSER;'
```

Erstellt die Datenbank, braucht aber ein `-d`, um sich überhaupt in den Cluster einloggen zu können (als postgres):
```
pg_restore --no-owner --no-privileges --role=ddluser --exit-on-error -C -d postgres soconfig.dmp
```

## Pub-DB
Rollen erstellen:
```
sudo -u postgres psql -d postgres -f create_roles.sql
```

Pub-DB-Dump einspielen (als postgres):
```
createdb pub
pg_restore --role=postgres --exit-on-error -d pub pub.dmp
sudo -u postgres psql -d postgres -c "ALTER DATABASE pub OWNER TO admin;"
```
