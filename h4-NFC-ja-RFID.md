## 1. Tarkastele käytössäsi olevia RFID tuotteita, mieti miten hyvin olet suojautunut RFID urkinnalta?

Jokapäiväisessä käytössä minulla on älypuhelin (Iphone) johon on tallentanut pankkikorttini, mutta kannan myös lompakkoa mukanani jossa on fyysinen pankkikortti. Kannan myös yleensä työavaimia mukana, joista löytyy kulkulätkä. 
Lompakko on ns. tavallinen lompakko eli sitä ei ole suojattu mitenkään RFID vakoilulta. Puhelimessa luotan puhelimen omaan suojaukseen ja yleisesti pieneen todennäköisyyteen koitua urkinnan kohteeksi.

## 2. Tutustu APDU komentojen rakenteeseen

APDU (Application Protocol Data Unit) on ISO/IEC 7816 -standardin mukainen viestintäprotokolla, jota käytetään älykorttisovellusten kanssa.

`CLA` = komentoluokka
`INS` = komento itse
`P1 ja P2` = komentojen parametrit
`Lc` = datan pituus
`Data` = lähetettävä data
`Le` = kuinka monta tavua odotetaan vastauksessa

## 3. RFID uutinen

https://www.rfidjournal.com/news/rfid-smart-access-cards-allow-instant-cloning-due-to-backdoor-report/221564/

Tietoturvayhtiö Quarkslab julkaisi raportin, jossa paljastuu tietoturvamurto MIFARE Classic älykorteissa. Fudan Microelectronicsin valmistamissa FM11RF08- ja FM11RF08S-korteissa on havaittu laitteistotason backdoor.
Haavoittuvuus mahdollistaa hyökkäyksen, jossa hyökkääjä tarvitsee fyysisen läheisyyden vain itse korttiin, ei kortinlukijaan tai taustajärjestelmään, jolloin kortin tiedot voidaan kopioida muutamassa minuutissa.

## Lähteet

RFID Smart Access Cards Allow Instant Cloning Due to Backdoor: Report: https://www.rfidjournal.com/news/rfid-smart-access-cards-allow-instant-cloning-due-to-backdoor-report/221564/

Application Protocol Data Unit (APDU): https://www.cardlogix.com/glossary/apdu-application-protocol-data-unit-smart-card/

Claude apuna kohdassa #2
