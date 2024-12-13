# h6 - Vuohi
## x) Lue ja tiivistä
**Karvinen 2023:**
- Karvisen artikkelissa on asennusohjeet WebGoattia varten.
- WebGoat on työkalu, jolla voit oppia web-penetraatiotestausta turvallisesti. Ohjelman käyttäminen vaatii teknistä osaamista sekä lailliset ja eettiset luvat.
- Sisältää ohjeen Javan asennukseen, palomuurin käyttöön ottoon ja WebGoatin asennukseen GitHubista.
- Muista käyttää WebGoatia vain laillisiin ja eettisiin tarkoituksiin.
## a) Asenna Webgoat 2023.4

Seurataan Karvisen artikkelin ohjeita. Java ja palomuuri olivat koneellani jo entisestään. Aloitin tehtävän varmistamalla onhan palomuuri aktiivinen.

![image](https://github.com/user-attachments/assets/cdf6f414-bcdf-4aa8-8896-62fbd7342758)

Ladataan Webgoat JAR.

![image](https://github.com/user-attachments/assets/4d0143f5-c5e2-4e05-bea1-43fee1f4ba9d)

Ajetaan WebGoat.

![image](https://github.com/user-attachments/assets/fd209322-9478-4da5-b37b-bd8031449188)

Mennään sivulle http://127.0.0.1:8888/WebGoat ja näin saadaan WebGoatin tehtävät näkyviin!

![image](https://github.com/user-attachments/assets/3c6731c8-dbc5-4c04-8653-0fe6f51f2e37)


## b) (A1) Broken Access Control WebGoat 2023.4
Varmistin ettei kone saa yhteyttä internettiin ja avasin Zapin. Aika aloittaa tehtävä **Hijack a session**. Ohjeissa puhuttiin istunnon varastamisesta keksien avulla. Yritin kirjautua omilla tunnuksilla ja kaappasin tästä aiheutuneen liikenteen. Avasin GET-pyynnön Zapissa ja ajattelin auttaisiko *hijack_cookie* arvon muuttaminen tehtävän ratkaisussa. 

![image](https://github.com/user-attachments/assets/a7590292-e080-46bd-84f7-91933093a3f9)

Vaihdoin numeroita kyseisestä keksistä ja lähetin pyynnön. Tässä saamani vastaus:

![image](https://github.com/user-attachments/assets/9cda5665-28ae-4593-964f-46563820defe)

Pyörittelin lukemattomia eri yhdistelmiä, mutta en päässyt sisälle. Jotenkin keksissä oleva väliviiva sai minut miettimään liittyisikö se käyttäjänimeen ja salasanaan mutta en ole ollenkaan varma asiasta. 

Tästä ei oikein tullut mitään joten siirrytään tehtävään **Insecure Direct Object References**. Tässä tehtävässä hyödynnetään URLia. Yritetään päästä sisään toiseen käyttäjään. 

Seurasin aluksi ohjeita WebGoatin sivuilla kunnes tuli tarve Zapille. Pitkän pyörittelyn jälkeen sain tälläisen vastauksen:

![image](https://github.com/user-attachments/assets/93f239f2-e250-4264-aaba-3f162219cd34)

En kuitenkaan ole vielä kenenkään käyttäjän sisällä.

# Lähteet
Karvinen, T. 2024. Tunkeutumistestaus - Penetration Testing course - 2024 late autumn. Saatavilla: https://terokarvinen.com/tunkeutumistestaus.

Karvinen, T. 2024. h6 - Vuohi. Saatavilla: https://terokarvinen.com/tunkeutumistestaus/#h6-vuohi. 

Karvinen, T. 2023. Try Web Hacking on New Webgoat 2023.4. Saatavilla: https://terokarvinen.com/2023/webgoat-2023-4-ethical-web-hacking/. 
