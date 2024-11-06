# h2 - Social sploit

## x)  Lue/katso/kuuntele ja tiivistä

**Jaswal 2020:**
- Kappaleessa on esimerkkihyökkäys jota käsitellään vaihe kerrallaan.
    - Hyökkäys yksittäiseen IP-osoitteeseen.
- On tärkeää kerrata yleisimpiä komentoja Metasploitissa:
    - Use
    - Show
    - Setg
    - Run
    - Exploit
- On todella tärkeää kerrata myös Meterpreter komentoja:
    - Sysinfo
    - Ifconfig
    - Arp
    - Shell
    - Getuid
- Metasploit on avoimen lähdekoodin ohjelma, mitä kehitetään jatkuvasti.
- Se on myös aika helppokäyttöinen.
- Hyökkäysten lopettaminen ja järjestelmästä poistuminen on turvallisempaa Metasploitilla.
## a) Harjoittelemme omassa virtuaaliverkossa, jossa on Kali ja Metasploitable

Kuten viime viikon raportissa ilmeni, minulla oli ongelmia saada Kali ja Metasploitable ottamaan yhteyttä toisiinsa. Tunnilla kuitenkin Karvisen kanssa keskustelun jälkeen minulle selvisi, että ongelmani piilee Host-only verkkoadapterissani.
Host-only adapter #2, jota käytin tehtävän suorittamiseen, oli vahingossa disabled muodossa. Tästä syystä koneet eivät kommunikoineet keskenään. Asetuksista tämän muuttamisen jälkeen, testasin saako koneet toisiinsa yhteyttä ja onnekseni ongelma oli näinkin pieni. 
Nyt kun oman huolimattomuudedn virheet ovat kohdattu, on hyvä lähteä suorittamaan uusia tehtäviä. 

Aloitan tehtävän testaamalla koneiden yhteyden ja varmistamalla sen, etteivät ne saa yhteyttä internettiin.

![image](https://github.com/user-attachments/assets/92049c05-26c0-449c-88fd-45f419e1d559)
![image](https://github.com/user-attachments/assets/63f9856b-5ecc-4c14-9253-d28832e0282d)

Koneet eivät saa yhteyttä internettiin! Testataan seuraavaksi koneiden välinen yhteys.

![image](https://github.com/user-attachments/assets/1791b6c0-4a3c-481b-81a4-242c1e2e75ac)
![image](https://github.com/user-attachments/assets/7eb0195a-c840-4b95-b58b-84b6df61fcf5)

Koneet saavat yhteyttä toisiinsa ja voimme siirtyä eteenpäin!

## b) Ota Metasploit msfconsole käyttöön
Metasploit msfconsole saadaan käyttöön komennolla ``sudo msfconsole``. 
![image](https://github.com/user-attachments/assets/dd5e7886-18fb-4eca-9d8e-0fa39959407c)

Tadaa! Metasploitable msfconsole on käytössä Kali koneella.
## c) Etsi Metasploitable porttiskannaamalla
Käytetään porttiskannaukseen komentoa ``db_nmap -sn 192.168.88.4``.
![image](https://github.com/user-attachments/assets/1ad1dc93-be7d-43e6-a5e3-2e3c9bb7fb43)

Jee! Maalikone löytyi!
## d)  Porttiskannaa Metasploitable perusteellisesti
Aloitan kohdan D tekemällä tehtävälle oman workspacen komennolla ``workspace -a h2``.

![image](https://github.com/user-attachments/assets/7266e021-10ae-405b-835e-62a282438ac3)

Onnistuneen luomisen jälkeen porttiskannataan Metasploitable ja tallennetaan tulokset kansioon *tehtava*.

Tähän käytetään komentoa ``nmap -oA tehtava 192.168.88.4``.

![image](https://github.com/user-attachments/assets/1be6925b-4dbd-48b5-a722-66de6a7835e2)

![image](https://github.com/user-attachments/assets/af36fa51-9019-46e8-97d5-71bf3d4c423b)

Tarkistetaan vielä onnistuiko tallennus kansioon *tehtava*.

![image](https://github.com/user-attachments/assets/44c6f775-fc20-4c7e-9305-7ad87268baa6)

## e) Tarkastele Metasploitin tietokantoihin tallennettuja tietoja
Käytetään tähän komentoja ``hosts`` ja ``services``. 

![image](https://github.com/user-attachments/assets/9e61cc3a-dd69-41af-b27c-efa58c676ecf)

![image](https://github.com/user-attachments/assets/d6d41d3a-896b-42cd-b680-4f264887a454)

## f) Vertaile nmap:n omaa tiedostoon tallennusta ja db_nmap:n tallennusta tietokantoihin
Nmap on tallentanut tiedot kolmeen eri tiedostoon; ne ovat tehtava.gnmap, tehtava.nmap ja tehtava.xml.

Ensimmäinen tiedostomuoto *.gnmap* on Nmapin perinteinen tekstitiedostomuoto, joka tuottaa perusraportin skannauksesta. Se sisältää yksityiskohtaisen listauksen skannatuista isäntäkoneista, avoimista porteista ja niiden palveluista, mutta ei ole yhtä jäsennelty kuin XML-muoto. Tämä tiedostomuoto voi olla hyödyllinen tavalliselle tarkastelulle, mutta Metasploit saattaa käsitellä sitä vähemmän tehokkaasti kuin XML-muotoista dataa. 

Tiedostomuoto *.nmap* on  tekstitiedostomuoto, joka tuottaa perusraportin skannauksesta. Se sisältää yksityiskohtaisen listauksen skannatuista isäntäkoneista, avoimista porteista ja niiden palveluista, mutta ei ole yhtä jäsennelty kuin XML-muoto. Tämäkin tiedostomuoto voi olla hyödyllinen tavalliselle tarkastelulle, mutta Metasploit saattaa käsitellä sitä vähemmän tehokkaasti kuin XML-muotoista dataa. 

Kolmas tiedostomuoto *.xml* on Nmapin XML-muotoinen skannausraportti. XML-muoto on erittäin jäsennelty ja koneellisesti luettava, ja se sisältää kaikki tiedot, joita Nmap voi kerätä. Tämä sisältää isäntäkoneet, avoimet portit, palvelut, versiotiedot, ja jopa muita yksityiskohtia, kuten skriptien tulokset. XML-muotoa käytetään usein tiedon tuomiseen ohjelmointirajapintojen kautta, kuten Metasploitin ``db_import`` komennolla, koska se sisältää koko tiedon ja on helppo käsitellä.
# Lähteet
*https://terokarvinen.com/tunkeutumistestaus/

https://terokarvinen.com/tunkeutumistestaus/#h2-social-sploit

https://learning.oreilly.com/library/view/mastering-metasploit/9781838980078/B15076_01_Final_ASB_ePub.xhtml#_idParaDest-31
