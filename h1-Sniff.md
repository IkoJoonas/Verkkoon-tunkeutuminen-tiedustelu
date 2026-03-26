## Laitteisto

Host : MacBook Air M2 2022 16Gt

Guest: Oracle VM VirtualBox 7.2.0

Virtuaalikone: Kali Linux -> Debian ARM 64

Ram: 8GB

Levytila: 40GB

CPU: 2 

## a) Linux

Olin asentanut Kali Linux jo aiemmin.

<img width="903" height="661" alt="Näyttökuva 2026-03-26 kello 16 10 58" src="https://github.com/user-attachments/assets/7f135f1f-36ab-4fd9-8a7f-821adcbdfe1a" />

## b) Ei voi kalastaa

Katkaisin Internet-yhteyden ja varmistin sen kokeilemalla pingaa Cloudfareen.

<img width="1124" height="148" alt="Näyttökuva 2026-03-26 kello 14 58 28" src="https://github.com/user-attachments/assets/8935355b-f6e4-43ff-be8f-66e8474f1c50" />

Palautin yhteyden ja kokeilin uudelleen.

<img width="1157" height="290" alt="Näyttökuva 2026-03-26 kello 14 57 55" src="https://github.com/user-attachments/assets/547750c5-68e3-49a6-b977-eb3c2331b4e4" />

## c) Wireshark

Wireshark oli valmiiksi asennettuna.

<img width="170" height="89" alt="Näyttökuva 2026-03-26 kello 14 59 45" src="https://github.com/user-attachments/assets/a78d40e4-849c-4f5c-a9de-259a91ffcc93" />

Liikenteen sieppaus:

<img width="1433" height="807" alt="Näyttökuva 2026-03-26 kello 15 04 08" src="https://github.com/user-attachments/assets/3a035cea-8728-4ab9-8507-9dc42b492af6" />

## d) Oikeesti TCP/IP

Link layer: Ethernet II

Internet layer: IPv4

Transport layer: TCP

Application layer: TLS

<img width="395" height="137" alt="Näyttökuva 2026-03-26 kello 16 22 57" src="https://github.com/user-attachments/assets/80a39655-6802-4430-8995-7a2c51629dd1" />

## e) Mitäs tuli surffattua?

DNS kysely, josta vastaukseksi ip osoite 216.58.210.164 joka vie google.com

<img width="1244" height="122" alt="Näyttökuva 2026-03-26 kello 15 21 00" src="https://github.com/user-attachments/assets/d6aeea46-b415-44a0-af90-9d2bb7f2ad6e" />

DNS kysely, josta vastaukseksi ip osoite 139.162.131.217 joka vie terokarvinen.com

<img width="1300" height="255" alt="Näyttökuva 2026-03-26 kello 15 23 07" src="https://github.com/user-attachments/assets/f6c2a67a-5d18-4778-b47a-476958738a64" />

Kaikki protokollat joita käytettiin: IPv4, QUIC, DNS, TCP, TSL ja ARP.

<img width="1044" height="284" alt="Näyttökuva 2026-03-26 kello 15 27 17" src="https://github.com/user-attachments/assets/3a0c3254-37c2-48f8-b155-f65935f6a533" />

Pakettien määrä: 283

Kaappaus kesti 7 sekunttia

<img width="873" height="775" alt="Näyttökuva 2026-03-26 kello 15 28 35" src="https://github.com/user-attachments/assets/28b19af5-fc2f-4c6f-b739-b84d5757aa44" />

TCP virhe.

<img width="968" height="755" alt="Näyttökuva 2026-03-26 kello 15 29 41" src="https://github.com/user-attachments/assets/a127a649-c018-4fda-903e-ce7fc8c4fa46" />
