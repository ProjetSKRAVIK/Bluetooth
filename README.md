# Bluetooth
Pour relier 2 cartes Arduino avec des modules Bluetooth type HC-05, il faut en définir une en esclave et une en maitre. Pour ceci, on téléverse les 2 programmes correspondants puis on utilise des commandes AT.

## Slave
  * AT pour vérifier que la communication fonctionne
  * AT+ROLE? pour verifier que son rôle est bien definit sur 0
  * AT+ADDR? pour obtenir son addresse

## Master
  * AT
  * AT+ROLE=1 pour definir sur Master
  * AT+CMODE=0 indique de se connecter toujours sur la même addresse
  * AT+BIND=addresse du slave
  
## Exemple pour le code

![foo](https://howtomechatronics.com/wp-content/uploads/2016/04/Communcation-Between-Two-HC-05-Bluetooth-Module-Circuit-Schematics.png "title")
