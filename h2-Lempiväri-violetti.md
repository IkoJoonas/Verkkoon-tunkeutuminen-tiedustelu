## Laitteisto

Host : MacBook Air M2 2022 16Gt

Guest: Oracle VM VirtualBox 7.2.0

Virtuaalikone: Kali Linux -> Debian ARM 64

Ram: 8GB

Levytila: 40GB

CPU: 2 

## x)

frjpoeäf

## a) Apache log. Asenna Apache-weppipalvelin paikalliselle virtuaalikoneellesi. Surffaa palvelimellesi salaamattomalla HTTP-yhteydellä, http://localhost . Etsi omaa sivulataustasi vastaava lokirivi. Analysoi yksi tällainen lokirivi, eli selitä sen kaikki kohdat. (Jos Apache ei ole kovin tuttu, voit tätä tehtävää varten vain asentaa sen ja testata oletusweppisivulla. Eli ei tarvitse tehdä omia kotisvuja tms.)

Aloitin tehtävän lataamalla apache2 palvelimen komennolla:
`sudo apt install apache2 -y`

Asentamisen jälkeen käynnistin palvelimen:
`sudo systemctl start apache2`

Avasin localhost sivun selaimessa

<img width="1202" height="446" alt="Näyttökuva 2026-04-07 kello 14 13 49" src="https://github.com/user-attachments/assets/ea32c2d0-dda6-43b0-a6c8-05c8b79d275e" />

Seuraavaksi tutkin logeja menemällä `cd /var/log/apache2`

Täällä ajoin komennon `tail -f access.log`

<img width="1174" height="177" alt="Näyttökuva 2026-04-07 kello 14 00 06" src="https://github.com/user-attachments/assets/8059b0f5-a020-436e-a906-6e093496b91e" />

Ensimmäisen lokirivin analysointi:

`127.0.0.1` on käyttäjän ip-osoite.

`GET / HTTP/1.1` on GET-pyyntö, jossa näkyy käyttäjän pyyntö palvelimelle ja käytetty protokolla.

`200 3383` on status coden 200 ja datan suuruuden 3383 yhdistelmä.

`Mozilla/5.0 (X11; Linux x86_64; rv:140.0) Gecko/20100101 Firefox/140.0` on käyttäjän User-Agent.

## b) Nmapped. Porttiskannaa oma weppipalvelimesi käyttäen localhost-osoitetta ja 'nmap -A' päällä. Selitä tulokset. (Pelkkä http-portti 80/tcp riittää)

Aloitin skannaamisen komennolla:
`sudo nmap -A -p 80 localhost`

<img width="788" height="412" alt="Näyttökuva 2026-04-07 kello 14 08 56" src="https://github.com/user-attachments/assets/b11c33c6-6b40-4822-8e01-13f3421a5078" />

`80/tcp open http` nähdään portin 80 olevan avoin ja palveluna on HTTP.

`Apache httpd 2.4.66 ((Debian))` käytössä olevan palvelimen tiedot.

`http-title: Apache2 Debian Default Page: It works` palvelu toimii.

`http-server-header: Apache/2.4.66 (Debian)` näyttää version headerissa.

`Device type: general purpose` eli tavallinen tietokone.

`Running: Linux 5.X|6.X
OS details: Linux 5.0 - 6.2` on käyttöjärjestelmä.

`Network distance: 0 hops` on sama tietokone eli localhost.
