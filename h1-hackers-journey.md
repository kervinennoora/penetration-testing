# h1 - Hacker's Journey

## x) Lue/katso/kuuntele ja tiivistä
**Herrasmieshakkerit:**
- Kuuntelin Podmesta jakson Tietoturvan Niksipirkka, vieraana Juho Rikala | 0x34.
- Jaksossa mainittiin CrowdStriken toimintahäiriö ja se kuinka siitä ei puhuttu BlackHatissa.
- Keskuteltiin siitä onko rikollinen tausta este vai meriitti it-alalla? Juontajat pääsivät siihen tulokseen, ettei varsinaisesti estettä ole, mutta luottamusta voi olla vaikea saada.
- Keskolla on pääkaupunkiseudulla sen ainut tietoturvatiimi. Tiimi kuitenkin toimii paljolti yhteistyössä muiden IT tiimien kanssa.
- Keräävät kulutustietoa vain luvanantaneilta asiakkailta. Tietoa käytetään tarjouksien räätälöimiseen ostotottumusten perusteella.
- EU:n direktiivit aiheuttavat aiheuttavat keskolle jatkuvasti töitä.
- K-plussa kortin saaminen ApplePay lomakkoon on työnalla, mutta ei lähitulevaisuudessa.

**Hutchins et al 2011:**
- Kill Chain eli tappoketju on malli, joka kuvaa kyberhyökkäyksen vaiheita hyökkäyksen suunnittelusta tavoitteiden saavuttamiseen
- Tämän mallin avulla kyberturvatiimit voivat paremmin havaita, torjua ja estää hyökkäyksiä ennen kuin ne onnistuvat tavoitteissaan.
- Sen vaiheita ovat:
  - Tiedustelu
  - Aseistus
  - Toimitus
  - Hyödyntäminen
  - Asennus
  - Komento ja hallinta
  - Tavoitteet
 
**Santos et al: The Art of Hacking:**
- Aktiivinen tiedustelu tarkoittaa tiedustelutoimenpiteitä, joissa hyökkäyskohteelle lähetetään tietoa, kuten porttien skannausta ja haavoittuvuuksien etsimistä.
- Usein nämä vaiheet ovat lainvastaisia jo itsessään.
- Yleisiä aktiivisen tiedustelun työkaluja porttien skannaukseen ovat esimerkiksi Nmap, Masscan ja Udpprotoscanner.
- Verkkosovellusten tutkimiseen EyeWitness on yleisin.
- Haavoittuvuuksien etsimiseen yleisimpiä ovat Nessus, Nexpose, Nikto ja Zed.

**KKO 2003:36:**
- Vuonna 1998 A yritti tunkeutua OP-ryhmän tietojärjestelmään Helsingissä käyttämällä porttiskanneria, jolla hän etsi avoimia välityspalvelimia.
- OP-ryhmä vaati A:lta vahingonkorvausta rikoksen selvityskustannuksista. Käräjäoikeus katsoi, ettei A ollut osoittanut selvää murtautumisaikomusta, joten se hylkäsi syytteen tietomurrosta, mutta tuomitsi hänet sakkoihin tietoliikenteen häirinnästä.
- Hovioikeus totesi myöhemmin, että A:n tarkoituksena oli tunkeutua järjestelmään, mikä teki teosta tietomurron yrityksen.
- Hovioikeus tuomitsi hänet korvauksiin osuuskunnalle ja sen alaiselle yhtiölle. Korkein oikeus vahvisti hovioikeuden päätöksen ja tuomitsi A:n
maksamaan täyden korvauksen tietoturvallisuusrikkomusten ennalta-arvattavista vahingoista.
## a) Asenna Kali virtuaalikoneeseen
## b) Irrota Kali-virtuaalikone verkosta
## c) Porttiskannaa 1000 tavallisinta tcp-porttia omasta koneestasi
## d) Asenna kaksi vapaavalintaista demonia ja skannaa uudelleen
## e) Asenna Metasploitable 2 virtuaalikoneeseen
## f) Tee koneiden välille virtuaaliverkko
## g) Etsi Metasploitable porttiskannaamalla
## h) Porttiskannaa Metasploitable huolellisesti ja kaikki portit
# Lähteet

Karvinen, T. 2024. Tunkeutumistestaus - Penetration Testing course - 2024 late autumn. Saatavilla: https://terokarvinen.com/tunkeutumistestaus/

Karvinen, T. 2024. h1 - Hacker's Journey. Saatavilla: https://terokarvinen.com/tunkeutumistestaus/#h1-hackers-journey

Hutchins, E. s.a. Intelligence-Driven Computer Network Defense Informed by Analysis of Adversary Campaigns and Intrusion Kill Chains. Saatavilla:https://lockheedmartin.com/content/dam/lockheed-martin/rms/documents/cyber/LM-White-Paper-Intel-Driven-Defense.pdf

Santol, O. 2019. The Art of Hacking (Video Collection). Saatavilla: https://learning.oreilly.com/videos/the-art-of/9780135767849/9780135767849-SPTT_04_00/

KKO:2003:36. Saatavilla:https://finlex.fi/fi/oikeus/kko/kko/2003/20030036
