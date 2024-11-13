# h3 - Nuuskija
## x) Lue ja tiivistä
**Popov 2024:**
- Hyvät ja laajat ohjeet Wiresharkin käyttöön. Kertoo kuinka näkee protokolla hierarkkiat, loppupisteet, DNS-tiedot.
- Kertoo myös eri suodattimista, TLS-purusta ja ABD-kommuikaatiosta.

**Karvinen 2023:**
- Karvisen tekkemä ohje ffufin hyödyntämiseen löytääkseen piilotettuja hakemistoja. Karvinen kertoo ohjeessaan kuinka ffuf Zuzzin avulla hyökätään maalikoneeseen.
- Ffuf on todella nopea.
- Karvinen on ohjeissaan myös luonut valmiiksi käytettävän kohteen, jonka voi ladata selaimesta.

## a) Valitse valmis hyökkäys
Tätä tehtävää varten valitsin helpotetun tehtävän. Henkilökohtaisen aikataulutus-ongelman takia tämä on paras ratkaisu. 

Otin yhteyttä maalikoneeseen Kalissa ja avasin VSFTPD-backdoorin. Sitä kautta pääsin käsiksi lähekoodiin. 

![image](https://github.com/user-attachments/assets/b6b5513d-33ec-4245-b712-bb41566a3b97)

## b) Sorsa

Kuvassa olevasta lähdekoodista ilmenee maalikoneen portti. Lähdekoodissa on varmasti paljon muutakin tärkeää tietoa, niistä keskusteltiin tunnilla. Itselleni ne eivät vielä auenneet täysin. 

## c) Snif snif

Toistetaan sama VSFTPD-hyökkäys ja kuunnellaan liikennettä Wiresharkilla.

Tässä kohtaa minulle kuitenkin ilmenee kasa ongelmia :(. Saan hyökkäyksen toimimaan oikein jos verkkoliikenteensnifferi ei ole päällä.
Virtuaalikokeeni saattaa olla jotenkin rikki, sillä heti kun kuuntelulaite on toiminassa. RHOST:tissa ilmenee yhteysongelmia. 
Kaikki onnistuu normaalisti, kunnes olisi aika antaa komento ``exploit``. Eli itse maalikoneeseen ei pääse käsiksi.

Lisäksi viestiliikenne näyttää erillaiselta verrattuna siihen, mitä testasin tunnilla. Tunnilla tehdessä liikennettä tuli esimerkiksi ARP ja TCP porteista. Tällä kertaa kuintekin liikenne näyttää tältä: 

![image](https://github.com/user-attachments/assets/c5cc41d5-eddf-4ab6-92d3-981c3222b150)

Rehellisesti sanottuna en oikein osaa tulkita kyseistä liikennettä. Sen tiedän, että MDNS on verkkoprotokolla, jota käytetään pienissä verkoissa. 
Täytyy tiedustella Teroa asiasta ja jos asia vaatii sen, poistan Kali koneen ja asennan sen uudelleen. 

## d)  Fuzzzz

Ratkaistaan Karvisen 2023 artikkelin dirfuz-1.

Aloitan syöttämällä ekat komennot Kalin terminaalissa.

![image](https://github.com/user-attachments/assets/889c8d2d-0cf5-4d6a-8c2b-27da4adface5)

Komentojen syötön jälkeen sain tämän vastaukseksi.

![image](https://github.com/user-attachments/assets/eaafc4da-e9f9-43fe-9d90-5834de360469)

Tämän jälkeen asennan ffufin Kaliin.

![image](https://github.com/user-attachments/assets/125b35ac-ca10-473a-a04b-b05cf80dd149)

![image](https://github.com/user-attachments/assets/de616167-5e52-404b-9638-aaec767a105c)

Ennenkuin irroitan koneen verkosta, latasin vielä ohjeessa mainitun hakemiston.

![image](https://github.com/user-attachments/assets/9e97d711-ae68-4787-b31e-a305a42ad16d)

Nyt kun kaikki valmistelu on tehty pääsen ffufaamaan! Testataan ensin, ettei kone saa yhteyttä verkkoon.

![image](https://github.com/user-attachments/assets/b3dd01e2-67e1-431d-ac49-105768202872)

Ja nyt päästään suorittamaan.

Tässä menikin sitten tovi, ja vastaus eroaa ohjeista. 

![image](https://github.com/user-attachments/assets/bf3297ae-7702-427d-b08e-90be89915395)

## e) HTB

Ekana ratkaisin kissan. Tässä tehtävässä ratkaistiin helppoja kysymyksiä. Lopussa täytyi löytää Root flag ja antaa sen vastaus. 

![image](https://github.com/user-attachments/assets/a3920927-112d-44a4-a7a2-83a40f68d23f)


# Lähteet
Karvinen, T. 2024. Tunkeutumistestaus - Penetration Testing course - 2024 late autumn. Saatavilla: https://terokarvinen.com/tunkeutumistestaus/

Karvinen, T. 2024. h3 - Nuuskija. Saatavilla: https://terokarvinen.com/tunkeutumistestaus/#h3-nuuskija

HackTricks. 2024. Wireshark tricks. Saatavilla: https://book.hacktricks.xyz/generic-methodologies-and-resources/basic-forensic-methodology/pcap-inspection/wireshark-tricks#improve-your-wireshark-skills

Karvinen, T. 2023. Find Hidden Web Directories - Fuzz URLs with ffuf. Saatavilla: https://terokarvinen.com/2023/fuzz-urls-find-hidden-directories/
