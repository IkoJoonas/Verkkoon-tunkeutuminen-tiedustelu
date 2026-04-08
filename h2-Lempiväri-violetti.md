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
