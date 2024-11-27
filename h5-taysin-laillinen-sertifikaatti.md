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
