## Laitteisto

Host 1: MacBook Air M2 2022 16Gt

Guest: Oracle VM VirtualBox 7.2.0

Virtuaalikone: Kali Linux -> Debian ARM 64

Ram: 8GB

Levytila: 40GB

CPU: 2 

Host 2: Suoritin: AMD Ryzen 7 1700 (8-Core Processor) RAM: 32 Gt Näytönohjain: 8 Gt Tallennustila: 932 Gt

Guest: Oracle VM VirtualBox 7.2.4

Virtuaalikone: Debian 13.3 Cinnamon

RAM: 4GB

Levytila: 20 GB

CPU: 2


## x) Lue ja tiivistä.

Hubacek 2019: Universal Radio Hacker SDR Tutorial on 433 MHz radio plugs

- Spectrum Analyzer:in avulla tarkitetaan taajuus.
- Signaali voidaan näyttää bitteinä, hexana ja ASCII muodossa.

Cornelius 2022: Decode 433.92 MHz weather station data

- Käyttämällä rtl_433 voidaan decodata 433 MHz taajuudet.
- URH voidaan käyttää tallentamaan ja analysoimaan signaaleja.

## a) Lähteet ja läppä

Tehty.

## b) rtl_433. Asenna rtl_433 automaattista analyysia varten. Kokeile, että voit ajaa sitä.

Asensin käyttämällä komentoa `sudo apt-get install rtl_433`

<img width="664" height="85" alt="Näyttökuva 2026-05-08 kello 12 48 02" src="https://github.com/user-attachments/assets/8b17a428-8b9e-4dda-a082-ac916c04b576" 

## c) Automaattinen analyysi. Analysoi näyte 'rtl_433' ohjelmalla.

Latasin annetun tiedoston ja analysoin sen.

<img width="745" height="366" alt="Näyttökuva 2026-05-08 kello 12 51 43" src="https://github.com/user-attachments/assets/1a5a7dde-9364-4230-9679-75341da7301c" />

Tiedostosta löytyi kolme laitetta `KlikAanKlikUit-Switch`, `Proove-Security` ja `Nexa-Security`. Kaikissa oli sama id/House Code.

## d) Too compex 16? Muunna näyte rtl_433-yhteensopivaan muotoon ja analysoi se.

Latasin annetun tiedoston. Vinkkien avulla päädyin kääntämään tiedoston seuraavanlaisesti:

`cp Recorded-HackRF-20250411_183354-433_92MHz-2MSps-2MHz.complex16s convertedHackRF_433.92M_2000k.cs8`

<img width="755" height="371" alt="Näyttökuva 2026-05-08 kello 13 01 38" src="https://github.com/user-attachments/assets/cb631e6c-63a2-4c3f-88dd-c7c21369a692" />

## e) Ultimate. Asenna URH, the Ultimate Radio Hacker. Tarkastele näytettä

Asensin urh:n :

`sudo apt-get -y install pipx`

`pipx install urh`

`pipx ensurepath`

Avasin ohjelman ja näyttee.

<img width="1595" height="1003" alt="urh" src="https://github.com/user-attachments/assets/221c4c5b-22aa-44eb-9ebc-d78ab864db5e" />

## f) Yleiskuva. Kuvaile näytettä yleisesti

- Kesto: 5.48s
- Taajuus: 433,912MHz
- Päivämäärä: 12.4.2025
- Kellonaika: 11.38.55
- Lisäksi näkyy kolme kohtaa, kun kaukosäätimen nappia on painettu ja signaali on lähtenyt.

## g) Bittistä.

Valitsin vasemmalta alhaalta kohdasta `Signal view` `Demodulated`.

Zoomasin ensimmäisen signaalin alkuun ja maalasin ensimmäinen nousun huipusta huippuun.

<img width="1597" height="590" alt="urh2" src="https://github.com/user-attachments/assets/dd07e319-4da1-4224-992d-b14b398ccf37" />

Valittuja kohtia oli 522 ja 522µs. Kysyin Claudelta mihin tätä voidaan verrata, vastaukseksi tuli 522 µs = 0,000522 sekuntia = noin puoli millisekuntia. Valo ehtii kulkea ~156 kilometriä
Valo kulkee tyhjiössä ~300 000 km/s, joten puolessa millisekunnissa se ehtisi Helsingistä melkein Ouluun.

## Lähteet

- Hubacek 2019:  Universal Radio Hacker SDR Tutorial on 433 MHz radio plugs. Katsottavissa: https://youtu.be/sbqMqb6FVMY?t=199 Katsottu 8.5.2026

- Cornelius 2022: Decode 433.92 MHz weather station data. Luettavissa: https://www.onetransistor.eu/2022/01/decode-433mhz-ask-signal.html Luettu: 8.5.2026.

- Karvinen Tero. Verkkoon tunkeutuminen ja tiedustelu. https://terokarvinen.com/verkkoon-tunkeutuminen-ja-tiedustelu/

- g)-kohdassa käytetty Claude.ai, "522µs: Miten pitkä yksi raakabitti on ajassa? Kuvaile tätä aikaa vertaamalla sitä johonkin"
