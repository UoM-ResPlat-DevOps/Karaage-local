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
