# Uhka-analyysi (uhkamallinnus) kansantajuisesti

Osittainen suomennos [OWASP:n uhka-analyysiohjeesta](https://www.owasp.org/index.php/Application_Threat_Modeling). Tarkoitus on saada aikaan toimiva, kansantajuinen suomennos uhka-analyysien tekemistä varten kotimaan IT-ammattilaisille. Apu on tervetullutta.


# Mikä on uhka-analyysi 

Uhka-analyysi, tai uhkamallinnus (threat modeling), pyrkii tunnistamaan ja dokumentoimaan järjestelmän kriittiset tiedot, rajapinnat, ulkoiset riippuvuudet ja tietovirrat. Järjestelmästä saadun ymmärryksen perusteella voidaan miettiä millaisia 
potentiaalisia uhkia järjestelmään kohdistuu, kuinka todennäköisiä ne ovat, mitä seurauksia on uhan realisoitumisella. [OWASP](https://www.owasp.org) tarjoaa ohjeessaan joitakin valmiita luokittelumalleja uhille ja varautumiskeinoille
suojautumista varten, joita on suomennettu alla.

## STRIDE-luokittelu

STRIDE ei ole ainoa menetelmä uhkien luokitteluun systemaattisesti, mutta se sopii Solitan tapauksessa kohtuullisen hyvin asiakasprojektien tarpeisiin. STRIDE tulee sanoista Spoofing, Tampering, Repudiation, Information disclosure, Denial of service, Elevation of privilege. Lyhennöskin voidaan toki suomentaa, mutta silloin on vaikeaa hahmottaa mikä on alkuperäinen lähde. Alla olevassa taulukossa on esitelty lyhyesti STRIDE-luokittelun sisältö.


| Tyyppi                 | Esimerkit                                                       | Kontrolli                         |
|------------------------|-----------------------------------------------------------------|-----------------------------------|
|Identiteettivarkaus (Spoofing) | Toisen käyttäjän tunnusten käyttäminen ilman lupaa. Tekeytyminen toiseksi käyttäjäksi. | Käyttäjien tunnistus, kirjautuminen (Authentication) |
|Peukalointi (Tampering) | Tiedon muuuttaminen, esimerkiksi tietokannan sisällön peukalointi tai verkon yli tapahtuvan tiedonsiirron sisällön manipulointi. | Tiedon eheys (Integrity) |
|Jäljitettävyys (Repudiation) | Toimintojen suorittaminen siten että jälkikäteen ei voida selvittää mitä on tapahtunut. | Kiistämättömyys (non-repudiation) |  
|Tietovuoto (Information disclosure) | Tietosisällön lukeminen luvatta, esimerkiksi siirrettäessä tietoa verkossa. | Luottamuksellisuus  (Confidentiality) |
|Palvelunesto (Denial of service) | Järjestelmän saattaminen tilaan, jossa sitä ei voida käyttää normaalisti. | Saatavuus (Availability) | 
|Käyttövaltuuksien laajentaminen (Elevation of privilege) | Käyttövaltuuksien ylittäminen, jotta voi päästä käsiksi tietoon tai toimintoon ilman lupaa.| Käyttöoikeudet/käyttövaltuudet (Authorization) | 


Uhat ja riskit pitää tunnistamisen myös analysoida. Se tarkoittaa, että jokainen uhka/riski todella ymmärretään priorisointia ja toimenpiteiden suunnittelua varten.
* Tunnistetaan reitit ja tavat, joilla riski voi realisoitua. Yksittäinen riski voi toteutua monesta syystä.
* Kun päästään riittävän syvälle niin kullekin syylle on löydettävissä kontrolli, esto tai muu varautumiskeino.

### Varautumiskeinot (mitigating controls)

| Uhkatyyppi | Varautusmiskeinoja |
|------------|--------------------|
|Identiteettivarkaus | 1. Sisäänkirjautuminen ja käyttäjien tunnistaminen |
|                    | 2. Salaisen datan suojaaminen |
|                    | 3. Salaisen datan jättäminen järjestelmän ulkopuolelle. |
|Peukalointi | 1. Käyttöoikeuksien toteutus ja mallinnus oikein |
|            | 2. Tiivistefunktioiden käyttö (hash function, hash algorithm) |
|            | 3. MAC (viestin allekirjoitus) |
|            | 4. Digitaaliset allekirjoitukset |
|            | 5. Peukalointiturvalliset protokollat (Tamper-proof protocol) |
|Jäljitettävyys | 1. Digitaaliset allekirjoitukset |
|               | 2. Aikaleimat |
|               | 3. Jäljitysketjun varmistaminen (audit trail) |
|Tietovuoto | 1. Käyttöoikeuksien rajaaminen |
|           | 2. Yksityisyyden takaavat protokollat |
|           | 3. Tiedon salaaminen (encryption) |
|           | 4. Salaisen datan suojaaminen |
|           | 5. Salaisen datan jättäminen järjestelmän ulkopuolelle. |
|Palvelunesto | 1. Sisäänkirjautuminen ja käyttäjien tunnistaminen |
|             | 2. Käyttöoikeuksien rajaaminen |
|             | 3. Tekninen suodatus (filtering) |
|             | 4. Kuristus-tekniikat (throttling) |
|             | 5. Palvelutason takaaminen (Quality of Service) -tekniikat |
|Käyttövaltuuksien laajentaminen | 1. Suoritetaan toiminnot matalimmalla sopivalla oikeustasolla. |

Jokaisesta varautumiskeinosta voisi kirjoittaa runsaasti kuvausta ja käytännön esimerkkejä siitä mitä asia käytännössä projektissa voi tarkoittaa, mutta taulukosta on apua kun asiasta keskustellaan ja mietitään erilaisia mahdollisia toimenpiteitä.

Olennaista on tehdä tietoinen päätös siitä mihin uhkiin halutaan varautua ja millä tavalla. Päätös voi olla myös jättää suojautumatta jotain uhkaa vastaan, mikäli se ei ole mielekästä 
uhan todennäköisyyden, vaikutuksen ja kustannusten analysoinnin perusteella.

## Uhkien sitominen riskienhallintaan

Uhkamallinnus on osa projektin riskienhallintaa, koska se on keino tunnistaa riskejä. Periaatteessa on viisi tapaa reagoida tunnistettuun uhkaan, joka muodostaa riskin projektille ja järjestelmälle:

1. Ei tehdä mitään. Toivotaan että mitään ikävää ei tapahdu.
2. Tiedotetaan riskistä. Esimerkiksi kerrotaan käyttäjille tunnetusta ongelmasta.
3. Lievennetään riskiä. Lisätään kontrolleja ja mekanismeja, joilla uhka ei muodosta niin isoa riskiä.
4. Hyväksytään riski tietoisella päätöksellä. Käytännössä johtoryhmän/tuoteomistajan asia päättää.
5. Siirretään riski toiselle osapuolelle. Esimerkiksi sopimuksen tai vakuutuksen avulla.
6. Poistetaan riski. Esimerkiksi luottokorttitiedot - päätetään että ei käsitellä järjestelmässä luottokorttitietoja.

Olennaista on päätöksenteossa erottaa riski, jonka uhka muodostaa tietojärjestelmälle siitä millaisen riskin uhka muodostaa operatiivisen toiminnan jatkuvuudelle. Riskienhallinnassa on tärkeää ajatella liiketoiminnan ja asiakkaan näkökulmasta riskiä, eikä hallita uhkia teknisinä ongelmina.



# Lisenssi

Solita Oy on tekijänoikeudenhaltija, tätä materiaalia saa käyttää Creative Commons, Attribution CC BY -lisenssin ehtojen mukaisesti.
[Pitkällinen juridinen teksti](/LICENSE)



 




