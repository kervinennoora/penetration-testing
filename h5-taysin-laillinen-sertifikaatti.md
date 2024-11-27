# h5 - Täysin Laillinen Sertifikaatti
## x) Lue/katso ja tiivistä

**OWASP 2021:**
- Brocken Access Control on noussut viidenneltä sijalta tärkeimmäksi haavoittuvuudeksi.
- 94% testatuista sovelluksista sisälsi jonkinlaisen rikkinäisen pääsynvalvonnan.
- Pääsynvalvonta varmistaa, että käyttäjät eivät voi toimia omien oikeuksiensa ulkopuolella. Sen epäonnistuminen voi johtaa luvattomaan tiedonpaljastukseen, tietojen muokkaukseen tai tuhoamiseen, tai liiketoimintafunktioiden väärinkäyttöön.
- Yleisiä haavoituksia:
    - Vähimmän oikeuden periaatteen rikkominen (kaikilla on pääsy, vaikka ei pitäisi).
    - Pääsynvalvonnan ohittaminen URL-osoitetta, sisäistä sovellustilaa tai HTML-sivua muokkaamalla.
    - Toisen käyttäjätilin tietojen katselu tai muokkaus suoraan tunnisteen kautta (IDOR).
    - API-pyyntöjen POST-, PUT- ja DELETE-toimintojen puuttuvat pääsynvalvonnat.
- Ehkäisykeinoja:
    - Deny by default: Oletuksena kaikki pääsy on estetty.
    - Rajaa Cross-Origin Resource Sharing (CORS) vain tarpeellisille toimijoille.
    - Poista hakemistolistaukset ja varmista, ettei palvelimella ole arkaluonteisia tiedostoja.
    - Rajoita API-pyyntöjä automaattisten hyökkäysten torjumiseksi.
 
- Server-Side Request Forgery:lla on suhteellisen alhainen esiintymistiheys, mutta testausta on tehty keskimääräistä enemmän, ja hyökkäyksen toteutus- ja vaikutuspotentiaalit ovat korkeita.
- SSRF-haavoittuvuuksia esiintyy, kun verkkosovellus hakee etäresurssia ilman käyttäjän antaman URL:n asianmukaista validointia. Hyökkääjä voi pakottaa sovelluksen lähettämään muokatun pyynnön odottamattomaan kohteeseen, jopa palomuurin, VPN:n tai muiden verkon käyttövalvontalistojen suojaamana.
- Ehkäisykeinot:
    - Verkkotaso:
         - Segmentoi etäresurssien käyttö erillisiin verkkoihin, jotta SSRF:n vaikutus pienenee.
         - Ota käyttöön "deny by default" -periaate palomuureissa ja salli vain välttämätön liikenne.
    - Sovellustaso:
         - Puhdista ja validoi kaikki käyttäjän syöttämät tiedot.
         - Poista HTTP-uudelleenohjaukset käytöstä.
         - Vältä kieltolistojen käyttöä SSRF:n ehkäisyssä – hyökkääjillä on työkaluja niiden ohittamiseen.
    - Lisätoimenpiteet:
         - Älä sijoita muita kriittisiä palveluita etujärjestelmiin (esim. OpenID).
         - Käytä erillisiä verkkosalausmenetelmiä (esim. VPN) korkean suojan tarpeisiin.

      
**PortSwigget Academy:**
- IDOR on pääsynvalvontahaavoittuvuus, joka ilmenee, kun sovellus käyttää käyttäjän antamaa syötettä suoraan resurssien käsittelyyn.
- IDOR liittyy tyypillisesti horisontaaliseen oikeuksien laajentamiseen, mutta se voi myös mahdollistaa vertikaalisen oikeuksien laajentamisen.
- IDOR on erityisen vaarallinen, koska:
    - Hyökkäykset ovat yksinkertaisia toteuttaa, usein vain URL-parametrin muuttamisella.
    - Se voi johtaa arkaluonteisten tietojen paljastumiseen ja vakaviin oikeuksien väärinkäyttöihin.
- Korjauksena tulee aina tarkastaa käyttäjän oikeudet suhteessa pyydettyyn resurssiin, ja suositeltavaa on käyttää epäsuoria tunnisteita (kuten tokenien tai satunnaisten tunnisteiden generoimista) suoran pääsyn sijasta.

  
- Path Traversal -haavoittuvuudet mahdollistavat hyökkääjän lukevan mielivaltaisia tiedostoja sovelluksen käyttävän palvelimen tiedostojärjestelmästä.
- Tämä sisältää:
    - Sovelluksen koodia ja dataa.
    - Tunnistetietoja taustajärjestelmille.
    - Herkkiä käyttöjärjestelmätiedostoja.
- Joissakin tapauksissa hyökkääjä voi myös kirjoittaa tiedostoihin, muuttaen sovelluksen toimintaa tai kaapaten palvelimen kokonaan.
- Ehkäisy:
    - Vältä käyttäjän syötteen välittämistä tiedostojärjestelmärajapintoihin. Suosi turvallisia vaihtoehtoja toteutukselle.
    - Käytä kahta puolustuskerrosta:
        - Syötteen validointi: Käytä sallittujen arvojen listaa tai varmista, että syöte sisältää vain hyväksyttyjä merkkejä (esim. aakkosnumeerisia).
        - Polun kanonisointi: Tarkista, että tiedoston kanoninen polku alkaa odotetulla peruskansiolla.
     
          
- Server-side template injection tapahtuu, kun hyökkääjä pystyy käyttämään mallipohjan natiivia syntaksia haitallisen hyökkäyksen suorittamiseen palvelimella.
- SSTI:n vaikutukset
    - Kriittinen vaara: Hyökkääjä voi saavuttaa etähallinnan palvelimeen, käyttää sitä muihin hyökkäyksiin tai varastaa tietoja.
    - Tietojen luku: Vaikka täysi hallinta ei ole mahdollinen, hyökkääjä voi silti lukea herkkiä tietoja ja tiedostoja palvelimelta.
- Ehkäisy:
    - Vältä suoraa käyttäjän syötteen lisäämistä malliin.
    - Käytä "logiikkavapaita" mallimoottoreita kuten Mustache, jotka erottavat esityksen ja logiikan toisistaan.
    - Sandboxaus.
    - Rajaa käyttäjien oikeuksia.
- SSTI:n ehkäisy vaatii huolellista suunnittelua, mutta oikein toteutettuna se voi merkittävästi pienentää palvelimeen kohdistuvien hyökkäysten riskiä.

- SSRF on verkkoturvallisuuden haavoittuvuus, jossa hyökkääjä voi saada sovelluksen tekemään HTTP-pyyntöjä ei-toivottuihin kohteisiin.
- SSRF-hyökkäysten vaikutukset
    - Antaa hyökkääjälle luvattoman pääsyn tietoihin tai toimintoihin.
    - Mahdollistaa jatkohyökkäykset muihin sisäisiin järjestelmiin.
    - Tehdä hyökkäyksistä näyttävän siltä, että ne ovat peräisin kohdeorganisaatiosta.
- Sokeassa SSRF:ssä sovellus suorittaa pyynnön, mutta hyökkääjä ei saa suoraa vastausta.
  
- Cross-site scripting (XSS) on verkkoturvallisuuden haavoittuvuus, jonka avulla hyökkääjä voi vaarantaa käyttäjän vuorovaikutuksen haavoittuvan sovelluksen kanssa.
- XSS:n avulla hyökkääjä voi:
    - Esittäytyä uhrikäyttäjänä ja suorittaa tämän oikeuksia vaativia toimintoja.
    - Päästä käsiksi kaikkiin tietoihin, joihin uhrikäyttäjällä on pääsy.
    - Jos uhri on sovelluksen ylläpitäjä, hyökkääjä voi saada täydellisen hallinnan sovelluksesta ja sen tiedoista.
- XSS toimii manipuloimalla verkkosivustoa niin, että se palauttaa haitallista JavaScript-koodia. Kun haittakoodi suoritetaan käyttäjän selaimessa, hyökkääjä voi täysin hallita käyttäjän vuorovaikutusta sovelluksen kanssa.
- Ehkäisy:
    - Syötteen suodatus
    - Tietojen koodaus
    - HTTP-vastausotsikot
    - Content Security Policy (CSP)
## a) Totally Legit Sertificate

Asensin OWASP ZAP sovelluksen virtuaalikoneelle viime tunnilla, josta johtuen sitä ei demota tässä raporissa. Siirryn siis suoraan CA-sertifikaatin luontiin.

Avataan OWASP ZAP ja mennään välisivulle Tools ja valitaan sieltä Options. Valitaan sieltä kohta Network, jonka alta löytyy Sever Cerificates.

![image](https://github.com/user-attachments/assets/266e3c8c-0de7-4c6f-ab45-8997c7571019)

Tallennetaan se ja siirrytään FireFoxin puolelle. Mennään asetuksiin ja haetaan certificates. Lisätään juuri tallentamamme Sertifikaatti FireFoxiin.

![image](https://github.com/user-attachments/assets/4bb04e5f-a493-4905-8c39-4ce818f0baa2)

Seuraavaksi muutetaan ZAPin asetuksia niin, että se kaappaa myös sivustojen kuvat. Palataan Options välisivulle ja tällä kertaa mennään kohtaan Display. Laitetaan ruksi kohtaan "Process images in HTTP requests/responses" ja tallenetaan muutos.

![image](https://github.com/user-attachments/assets/f309c916-fe80-4c21-99d0-3dc1fa8fa5f9)

Tämän jälkeen on aika siepata hakupyyntöjä.

![image](https://github.com/user-attachments/assets/f27afd6f-479d-45e0-926f-a2130cf10d69)

## b) Kettumaista

Asensin FoxyProxyn jo tunnilla, mutta asennuksen jälkeen sen pitäisi näyttää täältä.

![image](https://github.com/user-attachments/assets/c796adfd-194f-4125-b0f9-9c0b61eaeee1)

Luodaan uusi ZAP-proxy. Kuvassa näkyy kaikki proxyn tiedot, myös pattern joka sille on annettu koskien PortSwigger Labsia.

![image](https://github.com/user-attachments/assets/b4157ad9-c023-4f4b-bf52-1a05781f1d46)

Siepataan taas hakupyyntöjä.

![image](https://github.com/user-attachments/assets/782c73e9-f0ca-4bda-95ea-838be330f67c)

## Portswigger (kohdat c-j)

Kaikki tämän osan tehtävät ovat mainittuna lähteissä. 

**c)**

Tämä tehtävä käsittelee IDORia. Tehtävässä täytyy löytää salasana käyttäjälle *carlos* ja kirjautua käyttäjälle.

Mennään labissa sivulle *Live chat* ja lähetetään viesti. Tämän jälkeen painetaan "View transcript".

![image](https://github.com/user-attachments/assets/bd8cca30-2e76-43ce-9271-32e6f8229277)

Sillä välin Zap on tallentanut hakupyyntöjä ja sieltä löytyy GET-pyyntö. Pyynnössä määritellään mitä transcriptiä käytetään chatissa. Valitaan Get pyyntö ja siirrytään väilehdelle "Open/Resend with Request editor" Tällä hetkellä se on "6.txt", kokeillaan muuttaa se "1.txt".

![image](https://github.com/user-attachments/assets/2b12c729-de4f-41b8-99c9-89f8020b5df7)

Kun pyyntö on lähetetty. Näkee ZAPin avulla, että chat kaveri on antanut meille tarvittavan salasanan. 

![image](https://github.com/user-attachments/assets/0ca7a034-1744-4c54-abaf-826a76db45e3)

Nyt voimme kirjautua käyttäjälle *carlos*.

![image](https://github.com/user-attachments/assets/095166a2-a819-4867-8918-c1beda9268c3)

**d)**

Tässä tehtävässä käytetään hyväksi haavoittuvuuksia sivuston kuvissa. Tarjoitus saada selville */etc/passwd* tiedoston tiedot. 

Avataan lab ja klikataan joku tuotekuva auki. Samalla ZAP tallentaa hakupyyntöjä. 

Avataan GET-pyyntö request editorilla. Valitaan pyyntö, jossa näkyy kuvan arvo ja vaihdetaan siihen *../../../etc/passwd* ja lähetetään pyyntö. Vastauksena ZAP:ssa saadaan vastaus, jossa näkyy salattua tietoa. 

![image](https://github.com/user-attachments/assets/bb48b271-8745-4105-9302-9e5dfb24655b)

Kuvat sijaitsevat hakemistoissa. Muuttamalla kuvan hakemistoksi joku arkaluonteinen paikka, saadaan haavoittuvia tietoja esille. 

![image](https://github.com/user-attachments/assets/2abbba91-8639-4ad4-8e24-0259cf9d6e76)


**e)**

Tässäkin tehtävässä hyväksikäytetään kuvien haavoittumista. Mennään labiin ja avataan joku tuote auki. 

![image](https://github.com/user-attachments/assets/7bbcfa76-9cae-47d8-85a8-a524fea9bd6d)

Seurataan millaisia pyyntöjä ZAP on hakenut. Avataan GET-pyyntö request editorissa. Vaihdetaan kuvan arvoa.

![image](https://github.com/user-attachments/assets/d9913c35-e6db-47c1-9644-64879eb1d104)

Laitetaan kuvan arvoksi tällä kertaa */etc/passwd* ja lähetetään pyyntö. Tällä kertaa arvoksi annettin tarkka hakemisto, sillä käyttäjä on estänyt hakemistossa liikkumisen. 

![image](https://github.com/user-attachments/assets/579448d5-53c9-4b90-97ea-33d503c4a410)

Vastauksena saadaan lista salasanoista. 

**f)**

Tässä tehtävässä jatketaan samaa rataa, eli hyödynnämme kuvien haavoittumista. Avataan joku totekuva ja siirrytään ZAPin puolelle muokkaamaan hakupyyntöjä.

![image](https://github.com/user-attachments/assets/3965177c-4d64-4420-a244-63ae43d0abcc)

Request editorissa muokataan kuvan arvoksi *....//....//....//etc/passwd* ja lähetetään hakupyyntö. Tässä kohtaa katsoin vastauksen siitä missä muodossa hakemisto täytyy ilmoittaa, sillä "sequences" ei ole minulle hirveän tuttu juttu. 

![image](https://github.com/user-attachments/assets/c6fd3969-4ea4-457e-9fc7-eef164a0d536)

Lab suoritettu ja vastauksena lista salasanoista.

**g)**

Tässä tehtävässä on ideana ryöstää salaimen avain haitallisen koodin avulla. Ensimmäisenä kirjaudutaan käyttäjälle labissa. 

![image](https://github.com/user-attachments/assets/322efd4f-8467-445f-aa83-cbba8f2e1af2)

Olemme nyt sellaisella käyttäjällä, jolla on oikeus muokata tuotekuvia. Eli sitä hyödynnetään varmasti tässä tehtävässä. Tässä kohtaa olin aika hukassa, joten hyödynsin tehtävän annon mukana tulleita ohjeita/vastauksia. Ilman niitä en tätä olisi ratkaissut. 

Tehtävässä ideana muokata tuotekuvan kuvausta ja saada error-viesti.

![image](https://github.com/user-attachments/assets/da7e9c67-31cd-4443-bd24-d66cf01a544c)

Tämän vastauksen jälkeen kun tuotekuvausta muokataan uudelleen ja sinne laitetaan viesti *{{settings.SECRET_KEY}}*, antaa serveri vastaukseksi salaisen avaimen. 

![image](https://github.com/user-attachments/assets/b204f05b-2ce1-4e60-bcf0-25d83bf59aa7)

Tämä oli itselle aika haastava eli analysointi on hiukan hankalampaa. Mutta haitallisen koodin avulla saa selville arkaluontoista tietoa.

**h)**
Tämän tehtävän ohjeissa kerrotaan, että apuna käytetään varastosaldoa. Tehtävä on poistaa käyttäjä *carlos*

Kun labissa tarkastaa saldoa se tallentuu GET-pyyntönä ZAPiin. Muokkaamalla tätä pyyntöä pääsee sisälle. Ohjeissa kerrotaan, että se tapahtuu stockApin avulla. Vaidetaan request editorissa sen URLiksi *hhtp://localhost/admin*.

![image](https://github.com/user-attachments/assets/85701de4-8c9a-4328-8b4f-9089ae09f76d)

Vastaukseksi saadaan pätkä HTML-koodia. 

![image](https://github.com/user-attachments/assets/be43e895-0fb5-42ae-8060-d5d4031911a5)

HTML-koodista löytyy kohta kuinka poistaa käyttäjä. Kopioidaan se URLiin ja kokeillaan, poistuuko käyttäjä. 

![image](https://github.com/user-attachments/assets/28368ff1-8caa-4730-a641-d18aabe17560)

![image](https://github.com/user-attachments/assets/fca62c0a-c4b1-40ce-aea4-791936e6eb2e)

Ja näin lab saatiin ratkaistua ja *carlos* poistettua.

![image](https://github.com/user-attachments/assets/b937a71b-df21-43c0-bfc3-eb32f2986c5b)


**i)**

Tämän tehtävän tehtävänanto oli todella laihaa, joten siirryin suoraan siihen, että käytän apuna mallivastausta. Tehtävän ideana on käyttää hakukenttää hyökkäykseen. Jos hakukenttään kirjoittaa pätkän skriptiä, sivu ajaa sen. Labin sai suoritettua sillä, että kirjoitti hakukenttään *<script>alert(1)</script>*. 

Olen aika hämilläi tehtävästä.

**j)**


# Lähteet

Karvinen, T. 2024. Tunkeutumistestaus - Penetration Testing course - 2024 late autumn. Saatavilla: https://terokarvinen.com/tunkeutumistestaus/.

Karvinen, T. 2024. h5 - Täysin Laillinen Sertifikaatti. Saatavilla: https://terokarvinen.com/tunkeutumistestaus/#h5-taysin-laillinen-sertifikaatti.

OWASP.org. 2021. A01 Broken access Control - OWASP TOP 10:2021. Saatavilla: https://owasp.org/Top10/A01_2021-Broken_Access_Control/.

OWASP.org. 2021. A10 Server Side Request Forgery (SSRF) - OWASP TOP 10:2021. Saatavilla: https://owasp.org/Top10/A10_2021-Server-Side_Request_Forgery_%28SSRF%29/.

Portswigger.net. s.a. Insecure direct object references (IDOR) | Web Security Academy. Saatavilla: https://portswigger.net/web-security/access-control/idor.

Portswigger.net. s.a. What is path traversal, and how to prevent it? | Web Security Academy. Saatavilla: https://portswigger.net/web-security/file-path-traversal.

Portswigger.net. s.a. Server-side template injection | Web Security Academy. Saatavilla: https://portswigger.net/web-security/server-side-template-injection.

Portswigger.net. s. a. What is SSRF (Server-side request forgery)? Tutorial and examples | Web Security Academy. Saatavilla: https://portswigger.net/web-security/ssrf.

Portswigger.net. s. a. What is cross-site scripting (XSS) and how to prevent it? | Web Security Academy. Saatavilla: https://portswigger.net/web-security/cross-site-scripting. 

Portswigger.net. s. a. Lab: Insecure ogject references | Web Security Academy. Saatavilla: https://portswigger.net/web-security/access-control/lab-insecure-direct-object-references. 

Portswigger.net. s. a. Lab: File path traversal, simple case | Web Security Academy. Saatavilla: https://portswigger.net/web-security/file-path-traversal/lab-simple. 

Portswigger.net. s. a. Lab: File path traversal, traversal sequences blocked with absolute path bypass | Web Security Academy.  Saatavilla: https://portswigger.net/web-security/file-path-traversal/lab-absolute-path-bypass. 

Portswigger.net. s. a. Lab: File path traversal, traversal sequences stripped non-recursively | Web Security Academy. Saatavilla: https://portswigger.net/web-security/file-path-traversal/lab-sequences-stripped-non-recursively. 

Portswigger.net. a. s. Lab: Server-side template injection with information disclosure via user-supplied objects | Web Security Academy. Saatavilla: https://portswigger.net/web-security/server-side-template-injection/exploiting/lab-server-side-template-injection-with-information-disclosure-via-user-supplied-objects. 

Portswigger.net. s. a. Lab: Basic SSRF against the local server | Web Security Academy. Saatavilla: https://portswigger.net/web-security/ssrf/lab-basic-ssrf-against-localhost. 

Portswigger.net. s. a. Lab: Reflected XSS into HTML context with nothing encoded | Web Seurity Academy. Saatavilla: https://portswigger.net/web-security/cross-site-scripting/reflected/lab-html-context-nothing-encoded. 

Portswigger.net. s. a. Lab: Stored XSS into HTML context with nothing encoded | Web Security Academy. Saatavilla: https://portswigger.net/web-security/cross-site-scripting/stored/lab-html-context-nothing-encoded.
