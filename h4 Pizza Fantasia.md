# h4 Pizza Fantasia
## tehtävä X
Karvinen 2023: Configuration Management of Distributed Systems over Unreliable and Hostile Networks (pdf, ̣mirrors: local, archive.org), vain nämä kohdat:
4.12.1 Size and Complexity of Some DSLs (112. Ominaisuuksien määrä.)
*DSL(Domain Specific Languages) Ominaisuuksia löytyy enemmänkin kuin tarpeeksi
*Saltissa +500, Puppetissa +100
*Näihin vielä työkalujen omat erikoisuuspiirteet lisäksi.
Oma miete: Määrät tuntuvat valtavilta ja pistää miettimään onko mahdollista oppia kaikkea, mutta loppupeleissä käytetään vain pientä prosenttia ominaisuuksista.

4.12.2 Use of DSL Functions in Case Configuration (112-115. Mitä oikeasti käytetään.)
*Vain harvoja käytetään oikeasti. Muut ovat vain ylimääräistä
*Share n Type Commands
  20% 475 C case
  19% 429 F file
  10% 234 F package
  6% 136 F exec
  3% 75 F service
  3% 71 I fw::rules
  3% 67 I registry_value
  3% 66 C if
  3% 63 I registry::value
  3% 62 C class
  2% 52 C anchor
  2% 41 I packages::pkgdmg
  
  *Most used functions (F) and control structures (C) and internally defined (I) in Mozilla Release
Engineering Puppet manifests.
Oma miete: Miksi pitää olla näin älytön määrä kaikkea, kun alle 15 riittää kattamaan 77 prosenttia käytetyistä.

4.12.3.1 Dependencies Between Main Functions (115-117. Tärkeimmät rakennuspalikat.)


*Yleisimpiin toimintoihin kuuluvat paketti-tiedosto-palvelu (package-file-service), käyttäjä (user), ryhmä (group) ja komennon suoritus (exec).
*Category Functions
Daemon setup package, file, service
App setup package, file
User management user, group
File manipulation file, directory, symlink
*oma miete: Hallinta tuntuu kuitenkin toimivan melko vähäisillä toiminnoilla.


## Tehtävä A

Aloitettu tehtävän tekeminen pysäyttämällä (sudo systemctl stop apache2 nginx) ja disabloiimalla (sudo systemctl disable apache2 nginx). Tämän jälkeen tarkastin apache2 ja nginx tilan (sudo systemctl status apache2 ja sudo systemctl status nginx).
![Apache ja Nginx suljettu ja tarkastettu](https://github.com)
https://github.com/Macobra87/h1-Hei-Ansiblen-maailma/blob/main/suljettu%20ja%20otettu%20pois%20k%C3%A4yt%C3%B6st%C3%A4%20apache%20ja%20nginx%20ja%20tarkastettu%20niin%20olevan%20pois.jpg
• sudo systemctl stop apache2 nginx: Pysäyttää käynnissä olevat Apache- ja Nginx-verkkopalvelimet pääkäyttäjän oikeuksilla, jotta ne eivät varaa verkkoporttia 80.
• sudo systemctl disable apache2 nginx: Poistaa Apachen ja Nginxin automaattisen käynnistyksen käytöstä, jotta ne eivät käynnisty uudelleen tietokoneen uudelleenkäynnistyksen yhteydessä.
• sudo systemctl status apache2 (ja nginx): Tarkistaa palveluiden ajantasaisen tilan ja varmistaa, että molemmat ovat varmasti sammuneet (inactive).
Sitten pystyi suorittamaan asennuksen Lighttpd demoniin. Aloitin sudo apt-get update.
sitten vuorossa oli sudo apt-get install -y lighttpd https://github.com/Macobra87/h1-Hei-Ansiblen-maailma/blob/main/Lighttpd%20asennettu.jpg(en tiedä kauheasti demoneista joten kysyin google geminiltä (Gemini 4 Hydrogen), jonkun sopivan demonin asennettavaksi. Manuaalinen asennus onnistui
• sudo apt-get update: Päivittää järjestelmän pakettiluettelot ajan tasalle ennen uusien ohjelmistojen asentamista.
• sudo apt-get install -y lighttpd: Asentaa kevyen lighttpd-verkkopalvelindemonin järjestelmään ilman erillisiä vahvistuskysymyksiä (-y).
Testasin demonin toiminnan komennolla curl -I http://localhost, joka palautti tilakoodin HTTP/1.1 200 OKhttps://github.com/Macobra87/h1-Hei-Ansiblen-maailma/blob/main/lighttpd%20testaus.jpg
• curl -I http://localhost: Hakee paikallisen verkkopalvelimen HTTP-vastausotsikot ja todistaa palvelimen olevan toiminnassa (HTTP/1.1 200 OK).
https://github.com/Macobra87/h1-Hei-Ansiblen-maailma/blob/main/Ligttpd%20tarkastus.jpg

## Tehtävä B

Aloitin tehtävän luomalla Ansible-roolin kansiorakenteen (mkdir -p roles/lighttpd/{files,handlers,tasks}) ja kopioimalla toimivan oletusasetustiedoston roolin käyttöön (cp /etc/lighttpd/lighttpd.conf roles/lighttpd/files/lighttpd.conf).
• mkdir -p roles/lighttpd/{files,handlers,tasks}: Luo Ansible-roolille tarvittavat alihakemistot asetustiedostoille, handlereille ja tehtäville yhdellä komennolla.https://github.com/Macobra87/h1-Hei-Ansiblen-maailma/blob/main/Kansioiden%20handlerien%20ja%20teht%C3%A4vien%20luonti.jpg
• cp /etc/lighttpd/lighttpd.conf roles/lighttpd/files/lighttpd.conf: Kopioi alkuperäisen https://github.com/Macobra87/h1-Hei-Ansiblen-maailma/blob/main/Lighttpd%20kansiot.jpgasetustiedoston talteen roolin files-kansioon, jotta Ansible voi jakaa sen kohdekoneelle.
Tämän jälkeen loin roolin tehtävätiedoston (micro roles/lighttpd/tasks/main.yml), johon määrittelin package–file–service-rakenteen (paketin asennus, asetustiedoston kopiointi ja palvelun käynnistys), sekä handler-tiedoston (micro roles/lighttpd/handlers/main.yml) palvelun uudelleenkäynnistystä varten. Lisäksi päivitin päätiedoston (micro site.yml), jotta se ajaa roolit ["antero", "lighttpd"].
• micro roles/lighttpd/tasks/main.yml: Määrittelee Ansiblen suoritettavat tehtävät, joilla varmistetaan lighttpd-paketin asennus, asetustiedoston kopiointi ja palvelun päälläolo.
• micro roles/lighttpd/handlers/main.yml: Määrittelee uudelleenkäynnistystoiminnon, jonka Ansible suorittaa automaattisesti vain silloin, kun asetustiedosto muuttuu.
• micro site.yml: Määrittää kohdepalvelimen (localhost) ja listaa sille ajettavat roolit (antero ja lighttpd).
Lopuksi ajoin playbookin komennolla ansible-playbook -i hosts.ini site.yml -K. Ensimmäisellä ajolla apt-välimuistin päivitys epäonnistui, joten poistin update_cache: true -rivin tehtävätiedostosta ja ajoin playbookin uudelleen. Ajo onnistui virheittä (ok=10, changed=0, failed=0), mikä osoittaa konfiguraation olevan idempotentti ja valmiin.
• ansible-playbook -i hosts.ini site.yml -K: Suorittaa määritellyn Ansible-playbookin kohdekoneelle ja kysyy pääkäyttäjän sudo-salasanan (-K) ennen muutosten tekemistä.
https://github.com/Macobra87/h1-Hei-Ansiblen-maailma/blob/main/site.yml%20ajo.jpg
