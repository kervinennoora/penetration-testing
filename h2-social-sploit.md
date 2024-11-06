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
# Lähteet
https://terokarvinen.com/tunkeutumistestaus/

https://terokarvinen.com/tunkeutumistestaus/#h2-social-sploit

https://learning.oreilly.com/library/view/mastering-metasploit/9781838980078/B15076_01_Final_ASB_ePub.xhtml#_idParaDest-31
