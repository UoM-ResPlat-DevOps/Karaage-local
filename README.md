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
To override the default templates, place the replacement templates under

```
/opt/karaage/etc/Karaage3/templates
```
using the same directory and file names as the original template.

To maintain via this repository, the files under

```
/opt/karaage/etc/Karaage3/templates
```
are symbolically linked to the git versioned files.
