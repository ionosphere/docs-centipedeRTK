---
layout: default
title: Rover Windows
parent: Autres Rover RTK
nav_order: 5
---

## 5.2 Utilisation Rover RTK sur PC Windows

> Cette méthode est un exemple, il existe d'autres méthodes pour paramétrer un client Ntrip sous windows avec un récepteur F9P.
> L'objectif est d'intégrer les binaires Ublox plutôt que du NMEA, les paramètres du F9P sont quant à eux injectés à chaque lancement pour adapter facilement la configuration en fonction du travail à effectuer (Rate, Mask,DynModel,...). Le paramétrage est également plus fin afin d'avoir un FIX RTK rapide, stable et répétable.

**Toujours vérifier la disponibilité d'une base [Centipede](https://centipede.fr) avant de l'utiliser**

Pour l'utilisation sur le terrain, vous devez disposer d'un matériel compatible (antenne et récepteur) ainsi que d'une connexion Internet mobile (3-4-5G) pour la réception des trames de correction du caster [Centipede](https://centipede.fr)

### 5.2.1 Prérequis

#### Matériels

* Une tablette ou un PC sous windows 10

* Une [antenne GNSS bi-fréquence](https://store.drotek.com/da-910-multiband-gnss-antenna) ou bien la même chose chez un autre fournisseur [antenne GNSS bi-fréquence](https://www.ardusimple.com/product/simplertk2b/), d'autres modèles existent....

* Un [récepteur F9P](https://store.drotek.com/rtk-zed-f9p-gnss) ou bien la même chose chez un autre fournisseur [de récepteur F9P](https://www.ardusimple.com/product/survey-gnss-multiband-antenna/), d'autres modèles existent....

* Un [câble antenne sma mâle tnc mâle 3m (longueur à adapter en fonction de votre projet)](https://www.mhzshop.com/shop/Cables-et-cordons/Sur-mesure/50-ohms-WiFi-4G/Cordon-sur-mesure-en-coax-faible-perte-WLL-240-2-4-5-GHz-6-1mm.html) dans le cas où celui fourni avec l'antenne ne correspond pas à votre besoin.

#### Logiciels

* Le logiciel [Null-modem emulator](https://sourceforge.net/projects/com0com/files/latest/download) > création d'un virtual port COM pour utiliser les trames de géolocalisation NMEA corrigées en RTK comme un récepteur externe pour votre logiciel de collecte de donnée ou d'autoguidage.

* La dernière version du logiciel [RTKlib version Rtkexplorer demo5](http://rtkexplorer.com/downloads/rtklib-code/) > Calcul du positionnement en [RTK](https://fr.wikipedia.org/wiki/Cin%C3%A9matique_temps_r%C3%A9el) par [RTKlib](http://www.rtklib.com/) pour une géolocalisation centimétrique.

### 5.2.2 Update du récepteur F9P

Le récepteur F9P n'a pas toujours son [firmware](https://fr.wikipedia.org/wiki/Firmware) à jour quand on le reçoit, il est important de suivre cette procédure pour la suite:

* [Install U-center](https://www.u-blox.com/en/product/u-center) (Windows seulement)

* [Update F9P firmware](https://drotek.gitbook.io/rtk-f9p-positioning-solutions/tutorials/updating-zed-f9p-firmware)

### 5.2.3 Connexion et paramétrage

#### Paramétrage des ports COM et branchement de l'antenne GNSS

Il est nécessaire d'installer un virtual port COM sur windows pour récupérer la trame NMEA corrigée sur ce dernier.

* télécharger [Null-modem emulator](https://sourceforge.net/projects/com0com/files/latest/download) et l'installer.

* Une fois installé ouvrir le logiciel et vérifier les ports ouverts, dans l'exemple **COM9** reçois les messages et **COM 10** diffuse le message (NMEA)

![com](/assets/images/rover_w/1.PNG)

* Brancher l'antenne + récepteur F9P en USB

* Ouvrir ensuite le [gestionnaire de périphériques](https://support.microsoft.com/fr-fr/help/4026149/windows-open-device-manager) et vérifier les ports COM, dans l'exemple **COM9** et **COM10** comme précédemment expliqué et **COM7** le récepteur F9P en USB.

![com](/assets/images/rover_w/2.PNG)

> Repérez bien ces 3 Ports COM, il est indispensable de bien les identifier pour la suite du paramétrage en les adaptant à votre configuration, dans l'exemple:
> * **COM7**: Entrée USB de l'antenne GNSS
> * **COM9**: Sortie NMEA de RTKlib
> * **COM10**: Entrée NMEA pour AgOpenGPS ou de tout autre logiciel de géolocalisation
> Paramètres permanents. Il n'est pas nécessaire de réouvrir ce programme dans lors des prochains démarrages du PC.

#### RTKLIB

> RTKLIB permet de convertir le Signal de positionnement de l'antenne GNSS grâce à une correction RTCM3 (Réseau Centipede par exemple) en un signal de géolocalisation précise au centimètre si les conditions le permettent.

* Télécharger la dernière version de [RTKlib version Rtkexplorer demo5](http://rtkexplorer.com/downloads/rtklib-code/)
* le décompresser dans le dossier de son choix.
* Ouvrir RTKNavi

![RTKnavi](/assets/images/rover_w/3.PNG)

* Télécharger ce [fichier de paramétrage](https://raw.githubusercontent.com/jancelin/docs-centipedeRTK/master/assets/param_rtklib/RTKlib_windows.conf)
* cliquer sur **option ...**
* Cliquer sur **LOAD** et choisir le dernier [fichier téléchargé](https://raw.githubusercontent.com/jancelin/docs-centipedeRTK/master/assets/param_rtklib/RTKlib_windows.conf) et **OK**

> Permet de paramétrer automatiquement certains paramètres de RTkLIb

![RTKnavi](/assets/images/rover_w/a1.PNG)

* Cliquer sur le **I** en haut à droite
* cliquer sur **ROVER** > **Opt**

![RTKnavi](/assets/images/rover_w/4.PNG)

* Modifier si besoin le Port **COM7** (Entrée USB de l'antenne GNSS) en fonction de votre paramétrage.
* Télécharger ce [fichier de paramétrage](https://raw.githubusercontent.com/jancelin/docs-centipedeRTK/master/assets/param_rtklib/ZED-F9P.cmd)
* cliquer sur **ROVER** > **Cmd**

![RTKnavi](/assets/images/rover_w/a1.PNG)

* Cliquer sur **LOAD** et choisir le dernier [fichier téléchargé](https://raw.githubusercontent.com/jancelin/docs-centipedeRTK/master/assets/param_rtklib/ZED-F9P.cmd)
* Cocher **Commands at startup**

> Permet de charger des paramètres  injectés au module F9P à chaque démarrage

* Cliquer sur **Base Staion** > **Opt**
* Modifier le Mountpoint sur la base [Centipede](https://centipede.fr) la plus proche de vous.

> Si vous n'êtes pas couverts par une Base CentipedeRTK vous pouvez en fabriquer une [ici](/docs/base/).

![RTKnavi](/assets/images/rover_w/5.PNG)

* Cliquer sur le **O** en haut à droite
* cliquer sur **Solution** > **Option**
* Modifier si besoin le Port **COM9** (Sortie NMEA de RTKlib) en fonction de votre paramétrage.

![RTKnavi](/assets/images/rover_w/6.PNG)

* Faire **EXIT** et ré-ouvrir RTKNavi pour l'enregistrement des paramètres.


#### Premier démarrage

* Cliquer sur Start et attendre (de 30s à plusieurs minutes) une position **FIX RTK**

> L'antenne de réception doit bien sûr être en extérieur dans un milieu dégagé

* Si ce premier test apporte une solution en **FIX** passons à la suite.

![RTKnavi](/assets/images/rover_w/9.PNG)

### 5.2.4 Connexion pour [AgOpenGps](https://agopengps.discourse.group/)

* Ouvrir **AgOpenGPS** > **Paramètres de configurations**

* Sélectionner le Port GPS (Entrée NMEA pour AgOpenGPS dans l'exemple **COM10**) et la vitesse **115200**

* Cliquer sur **Connexion**

![RTKnavi](/assets/images/rover_w/11.PNG)
