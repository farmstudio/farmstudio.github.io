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

elindítani a ddev környezetet

    ddev start

be kell szerezni egy adatbázis dumpot és azt betölteni

    ddev import-db --src=letoltott-sql-file-neve.sql

*(ha zip-ben vagy gz-ben van letöltve az adatbázis, azt is 
meg lehet adni közvetlenül az import-db-nek, nem kell külön kicsomagolni)*

lásd KÓDÉPÍTÉS

ha sikerült, akkor itt be kell hogy töltsön az oldal:

- [http://projektneve.ddev.site](http://projektneve.ddev.site)


## Friss adatbázis betöltés

Ha van hozzáférésed az éles vagy a tesztoldal adminjához, le tudod tölteni az adatbázisát.

Lépj be az adminba

![Login](/img/login.png)

Töltsd le az adatbázist

![Login](/img/dbdump.png)

Töltsd be a letöltött adatbázist a ddev-be

    ddev import-db --src=c:\folder\letoltott-sql-file-neve.sql

## Kódépítés

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

frontend: javascript/css

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

