## Valmistelu

En saanut Moodlesta ladattua Mininettiä linkin kautta joten asensin sen alusta itse Mininetin sivuilta. Seuraavat komennot ovat ulkomuistista millä sain ympäristön valmiiksi tehtäviä varten.

`sudo apt update`

`sudo apt upgrade`

`sudo apt install python3-scapy`

`git clone https://github.com/ssam246/Network-Security-Lab.git`

`sudo apt install tar`

SSH-yhteyden saamisessa ja Xtermin käynnistämisessä oli myös ongelmia, mutta sain toimimaan käyttämällä:

`xhost +local:`

`ssh -X user@host`

Latasin Moodlesta labs.tar.gz tiedoston koneelleni ja siirsin sen Mininet VM sisälle ja purin sen komennolla:

`tar -xvf labs.tar.gz`

## a) Aja tunnilla esitetty ARP hyökkäys ja tutki, miten se toimii.

Otin SSH-yhteyden Mininettiin.

Kokeilin alkuun käynnistää verkko-ohjaimen komennolla `ryu-manager ryu.app.simple_switch_13`.

Tämä ei kuitenkaan toiminut, koska python3-ryu pakettia ei ollut asennettu.

Asensin sen `sudo apt install python3-ryu`

Suoritin kommenon `ryu-manager ryu.app.simple_switch_13` uudestaan.

<img width="499" height="185" alt="Sieppaa1" src="https://github.com/user-attachments/assets/fb33f969-7291-4aeb-870c-f54ffb84ff65" />

Avasin toisen terminaalin, jolla otin yhteyden Mininettiin.

Suoritin komennon `sudo -E mn --topo single,3 --mac --switch ovsk --controller remote` `-E` lisäyksenä materiaalissa annettuun komentoon, jotta sain toimimaan.
