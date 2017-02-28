Download Utility
----------------

Dieses AddOn schickt eine beliebige Datei aus dem Medienpool als Force-Download in den Browser.
Damit das AddOn funktioniert, muss folgende Zeile in die .htaccess:
<br>
```htaccess
# REWRITE RULE FOR SEO FRIENDLY DOWNLOAD URLS
RewriteRule ^download[s]?/([^/]*) index.php?download_utility=download&file=$1 [NC,L]
```

Platzier es bitte über oder unter
```
# REWRITE RULE FOR SEO FRIENDLY IMAGE MANAGER URLS
```
<br>
Falls du `nginx` nutzt, musst du folgendes in deine Config packen:
```htaccess
rewrite ^/download[s]?/([^/]*) /index.php?download_utility=download&file=$1 last;
```

Wie komm ich an die Downloadlinks?
---------------------------------------

```php
<?php
    echo DownloadUtility::getDownloadFile($filename = '', $rewrite = true);

    // Ausgabe: /download/dateiname.jpg
    // Falls rewrite auf false steht: index.php?download_utility=download&file=dateiname.jpg
?>
```

X-Send was???
---------------

Wenn dir

* X-SendFile
* X-Accel-Redirect

keine Begriffe sind, solltest du die Einstellung oben nicht aktivieren, denn der Download wird höchstwahrscheinlich nicht funktionieren. X-Send ist ein Apache / nginx / Lighttpd Mod, um (große) Dateien direkt über den Server abzuwickeln. Dieses Modul ist normalerweise nirgendswo per Default aktiv und nur für spezielle Umgebungen gedacht. Falls du dich damit auskennst und sicher bist, dass die Module aktiv sind, kannst du die Checkbox aktivieren, ansonsten lass sie bitte deaktiviert. Im deaktivierten Zustand werden die Dateien wie gewohnt über PHP ausgeliefert.


Falls die Mods installiert sind, muss folgendes in deine .htaccess (oder Apache/Nginx Conf):

```
XSendFile On
XSendFilePath /absoluter/pfad/bis/media
```
