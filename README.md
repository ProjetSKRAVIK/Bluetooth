# Communication entre les cartes Arduino

#### Nous voulons pouvoir communiquer a une carte arduino centrale toutes les informations collectées par les capteurs des cartes Arduino auxiliaires. Pour cela, plusieurs technologies sont possibles.
---

## Bluetooth
Pour relier 2 cartes Arduino avec des modules Bluetooth type HC-05, il faut en définir une en esclave et une en maitre. Pour ceci, on téléverse les 2 programmes correspondants puis on utilise des commandes AT.
#### 1. Slave
  * AT pour vérifier que la communication fonctionne
  * AT+ROLE? pour verifier que son rôle est bien definit sur 0
  * AT+ADDR? pour obtenir son addresse
#### 2. Master
  * AT
  * AT+ROLE=1 pour definir sur Master
  * AT+CMODE=0 indique de se connecter toujours sur la même addresse
  * AT+BIND=addresse du slave
#### 3. Exemple pour le code
![foo](https://howtomechatronics.com/wp-content/uploads/2016/04/Communcation-Between-Two-HC-05-Bluetooth-Module-Circuit-Schematics.png "title")

#### 4. Implémentation dans notre projet
Nous savons qu'il n'est pas possible pour un seul maitre de maintenir plusieurs connections en même temps. Nous pourrions donc stocker les informations des capteurs sur leurs cartes Arduino respectives les connecter une par une en Bluetooth a la carte centrale toutes les 5-10 minutes pour transmettre toutes les informations d'un coup. Ca permet de regler le problème des connections simultanées tout en s'assurant que les données sont presque tout le temps présentes sur la carte centrale. En cas de problème, seules les données des dernières minutes seraient perdues. En augmentant la frequence de transmission des données, les risques seraient encore plus réduits. Cette fréquence dépendra principalement du temps d'appairage de 2 modules Bluetooth.

---

## NRF24

Les modules NRF24 permettent d'envoyer et de recevoir des informations à distance avec très peu d'énergie sur la fréquence 2.4GHz. En associant chacuns de nos cartes Arduinos secondaires à ce type de module et une antenne, nous pourrions envoyer les données en temps réel vers la carte Arduino centrale. Nous avons donc besoin de 2 programmes différents. Nous utiliserons des liaisons SPI en définissant la carte Arduino centrale comme Master et les autres comme Slaves. Il existe déjà des bibliothèques dédiées aux modules NRF24 pour simplifier les connections et les échanges.

Il faut faire des test pour savoir si des informations sont perdues avec les programmes que l'on utilise car cette méthode de communication n'est pas extremement fiable.

