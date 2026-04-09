## Laitteisto

Host : MacBook Air M2 2022 16Gt

Guest: Oracle VM VirtualBox 7.2.0

Virtuaalikone: Kali Linux -> Debian ARM 64

Ram: 8GB

Levytila: 40GB

CPU: 2 

## x)

- Bianco 2013: Pyramid of Pain

  Pyramidi kuvastaa, että mitä korkeamman tason indikaattori torjutaan, sitä enemmmän se aiheuttaa hankaluuksia hyökkääjälle.

- Caltagirone et al 2013: Diamond Model

  Timanttimallin idea on analysoida kokonaiskuvaa hyökkäyksestä. Osa-alueina toimii hyökkääjä, toiminnallisuus, infra ja kohde.

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

## c) Skriptit. Mitkä skriptit olivat automaattisesti päällä, kun käytit "-A" parametria? (Näkyy avoimien porttinumeroiden alta, http-blah, http-blöh...).

`-A` on agressiivinen skannaus, johon kuuluu parametrit:

`-o` on käyttäjärjestelmän havainnointi

`-sV` on version skannaus

`-sC` on skriptien skannaus

`-traceroute` näyttää reitin minkä kautta paketit kulkeutuvat hostille

## d) Jäljet lokissa. Etsi weppipalvelimen lokeista jäljet porttiskannauksesta (NSE eli Nmap Scripting Engine -skripteistä skannauksessa). Löydätkö sanan "nmap" isolla tai pienellä? Selitä osumat. Millaisilla hauilla tai säännöillä voisit tunnistaa porttiskannauksen jostain muusta lokista, jos se on niin laaja, että et pysty lukemaan itse kaikkia rivejä?

Tarkastelin logeja uudestaan.

<img width="1178" height="747" alt="Näyttökuva 2026-04-07 kello 14 04 48" src="https://github.com/user-attachments/assets/8e3a5372-c46e-4810-abc4-25e98fc2b5bf" />

Nmap oli lähettänyt paljon erilaisia pyyntöjä mm. GET, POST ja OPTIONS.

Jos loki olisi laajempi voisi käyttää komentoja `grep -E 'nmap|Nmap'` tarkastelemiseen.

## e) Wire sharking. Sieppaa verkkoliikenne porttiskannatessa Wiresharkilla. Huomaa, että localhost käyttää "Loopback adapter" eli "lo". Tallenna pcap. Etsi kohdat, joilla on sana "nmap" ja kommentoi niitä. Jokaisen paketin jokaista kohtaa ei tarvitse analysoida, yleisempi tarkastelu riittää.

Käynnistin Wiresharkin ja sieppasin verkkoliikenteen.

Filtteröin näyttämään vain paketit joissa on sana "nmap" kirjoittamalla `Display filter` osioon `frame contains "nmap"`.

<img width="1436" height="775" alt="Näyttökuva 2026-04-07 kello 14 23 58" src="https://github.com/user-attachments/assets/6bc18119-9d5d-4a99-bdd0-18682b93bf3e" />

Nmap oli lähettänyt lukuisia pyyntöjä kuten GET /robots.txt , OPTIONS, POST ja PROPFIND.

Jokaisesta löytyi User-Agentin kohdasta, että nmap:iä on käytetty.

<img width="1072" height="278" alt="Näyttökuva 2026-04-07 kello 14 28 01" src="https://github.com/user-attachments/assets/93732792-9e67-4613-8574-a838c453e86f" />

## f) Net grep. Sieppaa verkkoliikenne 'ngrep' komennolla ja näytä kohdat, joissa on sana "nmap".

Aloitin verkkoliikenteen sieppaamisen käyttämällä komentoa `sudo ngrep -d lo -i nmap`

Tämän jälkeen avasin toisen shellin ja ajoin komennon `sudo nmap -A -p 80 localhost`

Ngrep sai kaapattua paljon liikennettä, mutta laitan tänne vain yhden kaappauksen, koska tiedoissa vaikutti olevan toistuvuutta.

<img width="763" height="650" alt="Näyttökuva 2026-04-07 kello 14 36 26" src="https://github.com/user-attachments/assets/006c8d2f-56f1-418b-85b0-0c6abf171b8e" />

`Access-Control-Request-Method` kertoo tulevien http-pyyntöjen metodit.

## g) Agentti. Vaihda nmap:n user-agent niin, että se näyttää tavalliselta weppiselaimelta.

Vaihdoin user-agenttia komennolla `sudo nmap localhost -A -p 80 -script-args http.useragent="BSD experimental on XBox350 alpha (emulated on Nokia 3110)"`

Tarkastelin logeja ja agentin muuttaminen oli onnistunut.

<img width="1211" height="767" alt="Näyttökuva 2026-04-07 kello 14 49 52" src="https://github.com/user-attachments/assets/e5da522a-b853-46c3-b6a0-6fe2a162fb54" />

## h) Pienemmät jäljet. Porttiskannaa weppipalvelimesi uudelleen localhost-osoitteella. Tarkastele sekä Apachen lokia että siepattua verkkoliikennettä. Mikä on muuttunut, kun vaihdoit user-agent:n? Löytyykö lokista edelleen tekstijono "nmap"?

Aloitin Wiresharkilla sieppaammisen ja käytin taas komentoa `sudo nmap localhost -A -p 80 -script-args http.useragent="BSD experimental on XBox350 alpha (emulated on Nokia 3110)"`

Tein filtteröinnin ja nyt olikin näkyvissä vain yksi nmap kohta ja User-Agent oli muuttunut viime kerrasta.

<img width="1440" height="458" alt="Näyttökuva 2026-04-07 kello 14 56 26" src="https://github.com/user-attachments/assets/47255a43-e22c-44c8-a8df-3fc87c5ce1c4" />

## i) Hieman vaikeampi: LoWeR ChEcK. Poista skritiskannauksesta viimeinenkin "nmap" -teksti. Etsi löytämääsi tekstiä /usr/share/nmap -hakemistosta ja korvaa se toisella. Tee porttiskannaus ja tarkista, että "nmap" ei näy isolla eikä pienellä kirjoitettuna Apachen lokissa eikä siepatussa verkkoliikenteessä. (Tässä tehtävässä voit muokata suoraan lua-skriptejä /usr/share/nmap alta, 'sudoedit'. Muokatun version paketoiminen siis rajataan ulos tehtävästä.)

Menin polkuun `/usr/share/nmap/` ja hain rivejä kommennolla `grep -ir "nmaplowercheck"` aikaisemman Wireshark tuloksen perusteella.

<img width="738" height="65" alt="Näyttökuva 2026-04-07 kello 15 00 27" src="https://github.com/user-attachments/assets/6a6348ec-4271-4c43-8214-ff627b44461a" />

Nanoa käyttäen lähdin muokkaamaan tiedostoa ja pitkän etsinnän jälkeen löysin kohdan joka oli näkynyt aiemmin.

<img width="624" height="83" alt="Näyttökuva 2026-04-07 kello 15 16 44" src="https://github.com/user-attachments/assets/f7ec6a3b-52fe-437c-ac20-049153772543" />

Muokkasin seuraavanlaisesti:

<img width="643" height="87" alt="Näyttökuva 2026-04-07 kello 15 40 24" src="https://github.com/user-attachments/assets/470bee9e-5d7a-4fcc-906f-a9c9025bab6a" />

Kokeilin olinko saanut siten, että nmap ei näy enää. Nollasin lokit kommennolla `sudo truncate -s 0 /var/log/apache2/access.log` ja tein skannauksen `sudo nmap localhost -A -p 80 -script-args http.useragent="BSD experimental on XBox350 alpha (emulated on Nokia 3110)"`

<img width="986" height="215" alt="Näyttökuva 2026-04-07 kello 15 44 46" src="https://github.com/user-attachments/assets/f45e8d29-f420-40ac-95e9-ac69c1be9bfd" />

<img width="1199" height="134" alt="Näyttökuva 2026-04-07 kello 15 48 56" src="https://github.com/user-attachments/assets/35fdbd36-5c72-4a9c-a35c-b4820bce2b4c" />

Olin onnistunut.

## j) FCC ID. Etsi valitsemasi langattoman laitteen tiedot FCC ID:llä. Mitä liikenteen purkamista tai manipuloimista hyödyttävää tietoa löydät?

Laitteeksi otin Jbl Go Essentialin, laitteen pohjasta löytyi teksti `FCC ID:APIJBLGOETL`.

Syötin nämä FCC sivulle

<img width="420" height="321" alt="jbl2" src="https://github.com/user-attachments/assets/407397e3-8293-40cf-ac1e-0f93be6cd809" />

Tulokseksi sain paljon hyödyllistä tietoa, kuten sisäiset ja ulkoiset kuvat.

<img width="691" height="271" alt="jbl1" src="https://github.com/user-attachments/assets/2f9f1101-ca4a-4b27-971b-a63abf2fb3be" />


## Lähteet

- Bianco 2013: Pyramid of Pain: https://detect-respond.blogspot.com/2013/03/the-pyramid-of-pain.html

- FCC: https://www.fcc.gov/

- Apache logs documentation: https://httpd.apache.org/docs/2.4/logs.html#accesslog

- Nmap documentation for Miscellaneous options: https://nmap.org/book/man-misc-options.html

- Access-Control-Request-Method header: https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Access-Control-Request-Method

