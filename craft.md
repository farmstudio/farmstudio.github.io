# Craft CMS + ddev üzemben tartás

## Kódfrissítés Quick Start Guide

Lejjebb részletesen le van írva, de ha már van egy működő projekted, ezzel frissítheted a kódot. Ha 400-as vagy 500-as hibát kapsz, akkor ezeket sorban futtatva valószínűleg megoldódik:

    git pull
    ddev start
    ddev exec composer install
    ddev exec ./craft migrate/all
    ddev exec ./craft project-config/sync
    ddev exec ./craft clear-caches/all
    npm install
    gulp build


## ddev telepítés első alkalommal

ha még nincs, telepíteni Docker-t meg DDev-et

- https://www.docker.com/products/docker-desktop
- https://ddev.readthedocs.io/en/stable/

átmásolni a .env.example-t .env-nek

    cp .env.example .env

és utána megcsinálni sorban az alábbiakat (adatbázis betöltés, kódépítés). Ha sikerült, akkor itt be kell hogy töltsön az oldal:

- [http://projektneve.ddev.site](http://projektneve.ddev.site)


## Friss adatbázis letöltés

Ha van hozzáférésed az éles vagy a tesztoldal adminjához, le tudod tölteni a friss adatbázisát.

Lépj be az adminba

![Login](/img/login.png)

Töltsd le az adatbázist

![Login](/img/dbdump.png)

## Adatbázis betöltés

Töltsd be a letöltött vagy fejlesztőtől kapott adatbázist a ddev-be

    ddev import-db --src=c:\folder\letoltott-sql-file-neve.sql

## Feltöltött file-ok szinkronizálása

Ha van hozzáférésed a szerverhez, letöltheted az adminon keresztül feltöltött kép stb. fileokat. Ezek általában a `web/assets` könyvtár alatt lesznek, ezeket a saját `web/assets` könyvtáradba töltsd.

## Kódépítés

### Backend: php és craft

Ha még nem fut a ddev, akkor elindítani

    ddev start

lehúzni az új kódot

    git pull

php csomagokat frissíteni

    ddev composer install

craft beállításokat, adatbázist szinkronizálni

    ddev exec ./craft migrate/all
    ddev exec ./craft project-config/sync
    ddev exec ./craft clear-caches/all

### Frontend: javascript és css

ha használ a projekt bowert (van `bower.json` a projektkönyvtárban)

    bower install

javascript csomagok telepítése

    npm install

front-end elemek építése (js, sass stb, feltéve hogy van jó gulpfile)

    gulp build

ha figyelni szeretnéd a változásokat, és a gulp fordítsa automatikusan:

    gulp watch


## Adatbázishoz kapcsolódás

    ddev describe

kiírja hogy milyen tudsz kapcsolódni phpMyAdminnal vagy egyéb klienssel, pl:

[phpMyAdmin](http://projektneve.ddev.site:8036)

## Kimenő levelek figyelése

[MailHog](http://projektneve.ddev.site:8025)

