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
# Lähteet
Karvinen, T. 2024. Tunkeutumistestaus - Penetration Testing course - 2024 late autumn. Saatavilla: https://terokarvinen.com/tunkeutumistestaus/

Karvinen, T. 2024. h3 - Nuuskija. Saatavilla: https://terokarvinen.com/tunkeutumistestaus/#h3-nuuskija

HackTricks. 2024. Wireshark tricks. Saatavilla: https://book.hacktricks.xyz/generic-methodologies-and-resources/basic-forensic-methodology/pcap-inspection/wireshark-tricks#improve-your-wireshark-skills

Karvinen, T. 2023. Find Hidden Web Directories - Fuzz URLs with ffuf. Saatavilla: https://terokarvinen.com/2023/fuzz-urls-find-hidden-directories/
