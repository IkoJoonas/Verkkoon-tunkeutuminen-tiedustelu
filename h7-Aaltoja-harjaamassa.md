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
