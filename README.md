# Karaage-local
Research Platform Services specific modifications to Karaage

```
https://github.com/Karaage-Cluster/karaage
```

## Locations
Karaage is run out of a container as a system service.  To review the locations that Karaage can see on the host system see:

```
/etc/systemd/system/karaage.service
```
By default, Karaage will search

```
/opt/karaage/etc/Karaage3/
```
for settings and local files before searching its paths.

## Templates
To override the default templates, the local empty location:

```
/opt/karaage/etc/Karaage3/templates
```

is mounted to the location of the git repository.

For example, if the repository is cloned to:

```
/opt/karaage/
```

then

```
/etc/systemd/system/karaage.service
```

should include the lines:

```
  -v /opt/karaage/etc/karaage3:/etc/karaage3 \
  -v /opt/karaage/Karaage-local/templates:/etc/karaage3/templates \
```
NOTE the order is important.

## Static files
Static files are aliased in the web-server settings (apache2 or httpd) to:

```
/opt/karaage/lib/karaage3/static
```

To include local static files, need to modify 

```
/etc/apache2/sites-available/default-ssl.conf
```

To redirect to git controlled css. Need to add redirect to:

```
/kgstatic/css/local
```

before the default `kgstatic` redirect.

For instance:

```
Alias /kgstatic/css/local "/opt/karaage/Karaage-local/static/css"
<Location "/kgstatic/css/local">
  SetHandler None
  <IfVersion >= 2.4>
  Require all granted
  </IfVersion>
</Location>
```

Before

```
Alias /kgstatic "/opt/karaage/lib/karaage3/static"
<Location "/kgstatic">
...
```

NOTE: The use of `css/local` is to allow the use of two locations with css files.  The templates will need to include the `local` directory

```
kgstatic/css/local/
```
