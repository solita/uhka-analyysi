# Uhka-analyysi kansantajuisesti

Osittainen suomennos [OWASP:n uhka-analyysiohjeesta](https://www.owasp.org/index.php/Application_Threat_Modeling). Tarkoitus on saada aikaan toimiva, kansantajuinen suomennos uhka-analyysien tekemistä varten kotimaan IT-ammattilaisille. Apu on tervetullutta.

# Mikä on uhka-analyysi

Uhka-analyysi pyrkii tunnistamaan ja dokumentoimaan järjestelmän kriittiset tiedot, rajapinnat, ulkoiset riippuvuudet ja tietovirrat. Järjestelmästä saadun ymmärryksen perusteella voidaan miettiä millaisia 
potentiaalisia uhkia järjestelmään kohdistuu, kuinka todennäköisiä ne ovat, mitä seurauksia on uhan realisoitumisella. OWASP tarjoaa ohjeessaan joitakin valmiita luokittelumalleja uhille ja varautumiskeinoille
suojautumista varten, joita on suomennettu alla.

## STRIDE-luokittelu

STRIDE ei ole ainoa menetelmä uhkien luokitteluun systemaattisesti, mutta se sopii Solitan tapauksessa kohtuullisen hyvin asiakasprojektien tarpeisiin. STRIDE tulee sanoista Spoofing, Tampering,
Repudiation, Information disclosure, Denial of service, Elevation of privilege. Lyhennöskin voidaan toki suomentaa, mutta silloin on vaikeaa hahmottaa mikä on alkuperäinen lähde.


| Tyyppi                 | Esimerkit                                                       | Kontrolli                         |
|------------------------|-----------------------------------------------------------------|-----------------------------------|
|Identiteettivarkaus (Spoofing) | Toisen käyttäjän tunnusten käyttäminen ilman lupaa. Tekeytyminen toiseksi käyttäjäksi. | Käyttäjien tunnistus, kirjautuminen |
|Peukalointi (Tampering) | Tiedon muuuttaminen, esimerkiksi tietokannan sisällön peukalointi tai verkon yli tapahtuvan tiedonsiirron sisällön manipulointi. | Integriteetti |
|Jäljitettävyys (Repudiation) | Toimintojen suorittaminen siten että jälkikäteen ei voida selvittää mitä on tapahtunut. | Kiistämättömyys |  
|Tietovuoto (Information disclosure) | Tietosisällön lukeminen luvatta, esimerkiksi siirrettäessä tietoa verkossa. | Luottamuksellisuus  |
|Palvelunesto (Denial of service) | Järjestelmän saattaminen tilaan, jossa sitä ei voida käyttää normaalisti. | Saatavuus | 
|Käyttöoikeudet (Elevation of privilege) | Käyttövaltuuksien ylittäminen, jotta voi päästä käsiksi tietoon tai toimintoon ilman lupaa.| Käyttöoikeudet | 


Uhat ja riskit pitää tunnistamisen myös analysoida. Se tarkoittaa, että jokainen uhka/riski todella ymmärretään priorisointia ja toimenpiteiden suunnittelua varten.
* Tunnistetaan reitit ja tavat, joilla riski voi realisoitua. Yksittäinen riski voi toteutua monesta syystä.
* Kun päästään riittävän syvälle niin kullekin syylle on löydettävissä kontrolli, esto tai muu varautumiskeino.

### Varautumiskeinot

| Uhkatyyppi | Varautusmiskeinoja |
|------------|--------------------|
|Identiteettivarkaus| 1. Sisäänkirjautuminen ja käyttäjien tunnistaminen |
|                   | 2. Salaisen datan suojaaminen |
|                   | 3. Salaisen datan siirtäminen järjestelmän ulkopuolelle. |
|Peukalointi | 1. Käyttöoikeuksien toteutus ja mallinnus oikein |
|            | 2. Hash-algoritmien käyttö |



# Lisenssi

Solita Oy on tekijänoikeudenhaltija, tätä materiaalia saa käyttää Creative Commons, Attribution CC BY -lisenssin ehtojen mukaisesti.
[Pitkällinen juridinen teksti](/LICENSE)



 




