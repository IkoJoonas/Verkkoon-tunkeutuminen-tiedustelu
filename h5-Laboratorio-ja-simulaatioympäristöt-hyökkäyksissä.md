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

<img width="727" height="256" alt="Sieppaa2" src="https://github.com/user-attachments/assets/ff1824a0-6a60-44dc-9167-b0f5cba5d3c2" />

Käynnistyi emulaatio, missä on päälaitteet h1, h2 ja h3.

Kokeilin, että yhteydet toimivat komennolla `pingall`.

<img width="326" height="95" alt="Sieppaa3" src="https://github.com/user-attachments/assets/6e873e10-95a3-4493-aeed-51abd1bf2282" />

Toimi.

Avasin h1 koneelle terminaalin komennolla `xterm h1`.

<img width="566" height="93" alt="Sieppaa4" src="https://github.com/user-attachments/assets/9c1b852c-e57f-4fee-be40-84748f0d78f0" />

Katsoin koneiden mac osoitteet komennolla `arp -n`.

<img width="566" height="131" alt="Sieppaa5" src="https://github.com/user-attachments/assets/5a4c59f9-bcdd-4c37-8644-538231561beb" />

Avasin h3 koneelle terminaalin komennolla `xterm h3` ja kytkin päälle IP Forwarding.

<img width="550" height="59" alt="Sieppaa6" src="https://github.com/user-attachments/assets/4b98ba07-44ca-47c5-82c1-65be63df1446" />

Seuraavaksi ohjasin h3 koneelle portin 22 tulevan liikenteen kulkeutumaan ulos myös portista 22, mikä tarkoittaa, että kone toimii nyt man-in-the-middle.


