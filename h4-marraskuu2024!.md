# h4 - Marraskuu2024!
## x) Lue ja tiivistä
**Karvinen 2022:**
- Karvisen artikkelissa kerrotaan siitä kuinka salasana hasheja voi murtaa Hashcatin avulla.
- Artikkelissa on asennusohjeet ja tietoa siitä kuinka identifioida hash-tyyppi.
- Lopuksi myös ohjeet murtamiseen ja Hashcatin tulosten analysointiin.

**Karvinen 2023:**
- Karvisen artikkelissa kerrotaan miten John the Ripperiä käytetään.
- Artikkeli sisältää asennusohjeet ja tehtävän salasanasuojatun ZIP-tiedoston murtoon.

**Santos et al 2017:**
- Videokokonaisuus hyökkäysten estämisestä ja korjauksesta.
- Salasanat täytyy pitää suojattuna varastoinissa sekä liikkeessä.
- Julkisten paikkojen Wifi-yhteyksien liikenne on harvoin salattua.
    - Helppo nuuhkia salasanoja.
- Salasanojen murtaminen nykyään helppoa johtuen laskentatehon noususta ja siitä, että ihmisillä on edelleen heikkoja salasanoja.
- Sanakirjoja voidaan käyttää hyödyksi salasanojen murtamisessa.
- Salasanojen suojausta täytyisi parantaa.
    - Paremmat tiivisteet
    - Suolaus
    - Pidemmät ja monimutkaisemmat salasanat
    - Kaksisuuntainen vahvistus
- John the Ripper on erinomainen työkalu salasanojen murtamiseen.
- Hashcat on nopeampi kuin John the Ripper.

**Polop et al 2024:**
- Käytettäviä komentoja esimerkiksi:
    - ``msfvenom -p <PAYLOAD> -e <ENCODER> -f <FORMAT> -i <ENCODE COUNT> LHOST=<IP>``
    - ``msfvenom -p linux/x86/meterpreter/bind_tcp RHOST=(IP Address) LPORT=(Your Port) -f elf > bind.elf``
 
## a)  Asenna Hashcat ja testaa sen toiminta murtamalla esimerkkisalasana

Ennen tämän viikon kotitehtäviä poistin Kali virtuaalikoneen omalta koneeltani ja asensin uudelleen. Kone käyttäytyy nyt huomattavasti paremmin ja uskon sen vaikuttavan positiivisesti tämän viikon tehtävien tekoon.

Aloitetaas tehtävä asentamalla Hashcat Karvisen ohjeiden mukaisesti.

![image](https://github.com/user-attachments/assets/fc56d550-4a67-40f1-8a75-d554b56ce2de)

Luodaan uusi hakemisto *hashed* ja ladataan sinne sanakirja hakemisto *Rockyou*.

![image](https://github.com/user-attachments/assets/ea4e68dd-6732-4d7b-a5a5-e0028f38957d)

Käytetään komentoa ``hashcat -m 0 '6b1628b016dff46e6fa35684be6acc96' rockyou.txt -o solved`` ja murretaan Hash. 

![image](https://github.com/user-attachments/assets/66a335d1-0379-458d-9509-ef0971d3712b)

Saatiin haluttu lopputulos eli salasana on summer.

![image](https://github.com/user-attachments/assets/7d0cf121-5fe4-4f50-ac64-7c05bdaebcf8)


# Lähteet
Karvinen, T. 2024. Tunkeutumistestaus - Penetration Testing course - 2024 late autumn. Saatavilla: https://terokarvinen.com/tunkeutumistestaus/

Karvinen, T. 2024. h4 - Marraskuu2024!. Saatavilla: https://terokarvinen.com/tunkeutumistestaus/#h4-marraskuu2024

Karvinen, T. 2022. Cracking Passwords with Hashcat. Saatavilla: https://terokarvinen.com/2022/cracking-passwords-with-hashcat/

Karvinen, T. 2023. Crack File Password With John. Saatavilla:  https://terokarvinen.com/2023/crack-file-password-with-john/

Santos, O. 2017. Security Penetration Testing The Art of Hacking Series LiveLessons. O'Reilly. Saatavilla: https://www.oreilly.com/videos/security-penetration-testing/9780134833989/9780134833989-sptt_00_06_00_00/

HackTricks. 2024. MSFVenom - CheatSheet. Saatavilla:  https://book.hacktricks.xyz/generic-methodologies-and-resources/reverse-shells/msfvenom
