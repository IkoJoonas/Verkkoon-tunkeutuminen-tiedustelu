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

Seuraavaksi ohjasin h3 koneelle portin 22 tulevan liikenteen kulkeutumaan ulos myös portista 22, mikä tarkoittaa, että kone toimii nyt man-in-the-middle. Käytin komentoa `iptables -t nat -A PREROUTING -p tcp --dport 22 -j REDIRECT --to-port 22`.

Aloitin h3 verkkoliikenteen kuuntelun.

<img width="567" height="70" alt="Sieppaa7" src="https://github.com/user-attachments/assets/fa002c36-e6c0-4a44-beb2-64898f7140a0" />

Asensin sshesame:n komennolla `sudo apt install sshesame`.

Käynnistin sen.

<img width="566" height="79" alt="Sieppaa8" src="https://github.com/user-attachments/assets/5904cf8b-3750-4dcc-9f61-0cdb66365a8d" />

Jätin taustalle ja avasin uuden terminaalin h3.

Suoritin komennon `python3 ./arp_poison.py` joka muuttaa verkon laitteiden ARP-tauluja.

Menin takaisin h1 terminaaliin ja otin SSH-yhteyden h2 koneelle.

Takaisin h3 terminaalissa, jossa sshesame oli käynnissä näkyi lokitietoja mm. salasana.

<img width="567" height="210" alt="Sieppaa9" src="https://github.com/user-attachments/assets/afc0f5cc-7a5e-4a08-9e21-db696d15e8b1" />

Tarkastin ARP-taulun uudelleen ja siellä oli tapahtunut muutos koneen h2 MAC-osoitteessa.

<img width="570" height="93" alt="Sieppaa10" src="https://github.com/user-attachments/assets/44e2f35e-b9e0-4c6d-b509-02952f18a327" />

## b) ICMP Spoofing ja TCP Session Hijacking. Aja molemmat labrat läpi ja kerro, miten molemmat tekniikat toimivat.

ICMP Spoofing = Hyökkääjä lähettää ICMP-paketteja (Internet Control Message Protocol), mutta väärentää lähettäjän IP-osoitteen.

Käynnistin verkko-ohjaimen ja mininet uudestaan.

`ryu-manager ryu.app.simple_switch_13`

`sudo -E mn --topo single,3 --mac --switch ovsk --controller remote`

Avasin terminaalit h1 ja h2.

Tarkistin koneen h1 IP-osoitteen, jotta pystyn pingata siihen koneelta h2. IP oli 10.0.0.1

Aloitin h2 pingin koneelle h1 `ping 10.0.0.1` ja samalla suoritin h1 komennon `python3 ./sniff_icmp.py`

<img width="512" height="67" alt="2Sieppaa" src="https://github.com/user-attachments/assets/8a9d5144-f61a-4f46-ab59-db31acc7aeaf" />

ICMP echo-request tulee osoitteesti 10.0.0.2 eli koneesta h2.

Seuraavaksi avasin toisen h1 terminaalin ja suoritin komennon `python3 ./spoof_icmp.py` samalla, kun toisessa h1 terminaalissa oli `python3 ./sniff_icmp.py` käynnissä ja h2 `ping 10.0.0.1`.

<img width="515" height="93" alt="2Sieppaa1" src="https://github.com/user-attachments/assets/5a2ffd71-a9a2-4c81-bca7-01cb2b1cf1b1" />

Nyt ICMP echo-reply on kaksi peräkkäin, koska `spoof_icmp.py` lähettää lisäksi oman echo viestin h2 koneelle.

TCP Session Hijacking = Hyökkääjä ottaa haltuunsa olemassa olevan TCP-yhteyden kahden osapuolen välillä.

Käynnistin verkko-ohjaimen ja mininet uudestaan.

`ryu-manager ryu.app.simple_switch_13`

`sudo -E mn --topo single,3 --mac --switch ovsk --controller remote`

Avasin terminaalit h1, h2 ja kaksi h3.

Käynnistin h1 terminaaliin palvelimen komennolla `python3 ./tcp_server.py`.

<img width="503" height="40" alt="2Sieppaa2" src="https://github.com/user-attachments/assets/695d96dd-fc0a-4b49-a768-c628c335011b" />

Ja h2 terminaaliin clientin komennolla `python3 ./tcp_client.py`.

<img width="511" height="52" alt="2Sieppaa3" src="https://github.com/user-attachments/assets/e1c2d821-51fc-4d5e-a651-7e58339baa1e" />

Toisessa h3 terminaalissa käynnistin kuuntelun komennolla `python3 ./sniff_tcp_session.py`.

<img width="553" height="39" alt="2Sieppaa5" src="https://github.com/user-attachments/assets/819de544-3f41-491f-8f1c-502e62fe01b1" />

Ja toisessa TCP-yhteyden kaappauksen komennolla `python3 ./tcp_hijack.py`.

<img width="509" height="50" alt="2Sieppaa4" src="https://github.com/user-attachments/assets/ebf184e7-f621-4aa2-b0d7-56868d25b2af" />


## c) 02-SDN-DDos_Simulation tryout TCP SYN-Flood-hyökkäys

TCP SYN-Flood-hyökkäys = TCP SYN flood on palvelunestohyökkäys (DoS), jossa kohdejärjestelmä ylikuormitetaan lähettämällä valtava määrä TCP-yhteyden aloituspyyntöjä (SYN), mutta yhteyttä ei koskaan viimeistellä.

Menin kansioon `/labs/02-SDN_DDoS_Simulation-tryout/`.

Käynnistin verkon komennolla `sudo python3 simple_tree_top.py`.

Ajoin hyökkäyksen komennolla `sudo python3 tree_topology.py`.

<img width="456" height="137" alt="3Sieppaa" src="https://github.com/user-attachments/assets/fc90fdcb-e7ef-42c0-a865-9e72d4c7debd" />

<img width="452" height="64" alt="3Sieppaa1" src="https://github.com/user-attachments/assets/2509efc3-f2dc-4b04-bd62-e1562c7dd6e1" />

Komento loi kymmeniä simulaatioita, joissa isäntäkoneet vuorotellen suorittivat hyökkäyksiä ja lähettivät normaaleja pyyntöjä.

## Lähteet

- Network-Security-Lab: https://github.com/ssam246/Network-Security-Lab
- Download/Get Started With Mininet: https://mininet.org/download/
- MobaXterm: https://mobaxterm.mobatek.net/
- Moodle
- ChatGPT selittämään miten tekniikat toimivat
