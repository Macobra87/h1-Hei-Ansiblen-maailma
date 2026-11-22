# h5 Gitar Hero
## Tehtävä x

Tiivistelmä
Chacon & Straub (2014): Pro Git, 2ed – luku 1.3 Getting Started - What is Git?
*Git ei tallenna muutoksia rivi rivilta vaan ottaa snapshotin muutoksista.
*Lähes kaikki toiminta tapahtuu paikallisesti ja on tästä syystä melko nopeaa.
*Kaikki tarkistetaan (checksum) ennen tallennusta. Tiedostoja ei voi muuttaa tai korruptoida Gitin huomaamatta.
*Git vain lisää dataa.
*Gitissä 3 tilaa: 
Modified: muokattu mutta ei tallennettu databaseen.
Staged: merkattu odottamaan committia.
Committed: Tallennettu paikalliseen databaseen.

Git Komennot
Gitin käyttö on lähinnä 'git add --all && git commit; git pull && git push'
Hyödysin https://git-scm.com/ sivuston https://git-scm.com/cheat-sheet Cheat sheetiä ja sivuston muita selityksiä löytääkseni sopivat kuvaukset noihin komentoihin, nämä toimi kaikkiin muihin kohtiin paitsi && ;: jotka löytyi man bash kautta ja sain sieltä sopivan ohjeistukset ja selitykset.
• git add --all: Lisää uudet, muokatut ja poistetut tiedostot staging-alueelle odottamaan seuraavaa tallennusta (committia).
• &&: Bash komento joka Siirtyy ja toteuttaa seuraavan toimenpiteen jos edellinen onnistuu ongelmitta.
• git commit: Tallentaa staging-alueelle merkityt muutokset pysyväksi Git-tietokantaan.
• ;: Komentojen erotin: suorittaa seuraavan komennon riippumatta siitä, onnistuiko edellinen komento vai ei.
• git pull: Hakee etävarastosta uusimman tallennuksen.
• git push: Lähettää omat paikalliset commitit etävarastoon kaikkien nähtäville.

## Tehtävä A

Luotu uusi varasto githubiin.
Aloitettu etsimällä kohta; Create a new repository.
annettu nimi NOsunshine ja kuvaus practiseSunshine.
Otettu tehtävästä kuvat luonti osiosta ja luodusta repositorystä. Tämän jälkeen kopioin vihreän Code napin alta SSH linkin.
Lisätty oikeudet githubiin asetuksista.


## Tehtävä B

Kloonattu onnistuneesti tehty kansio Debianiin git clone git@github.com:Macobra87/NOsunshine.git. tämän jälkeen muokattu README.md tiedostoa. muutoksen jälkeen git add --all jonka jälkeen commit. Tehty nimetty testi ja sitten push komennolla siirretty tehdyt muutokset eteenpäin. Tulokset löytyivät githubista.

## Tehtävä C

Aloitin tehtävän tekemällä `README.md`-tiedostoon tarkoituksella huonon muutoksen ilman committia (`echo "Huono testi ilman committia" >> README.md`) ja tarkistamalla tilan komennoilla `cat README.md` sekä `git status`. Tämän jälkeen tuhosin tallentamattoman muutoksen pysyvästi komennolla `git reset --hard`, jolloin tiedosto palautui täsmälleen edellisen commitin mukaiseen tilaan.

* **git status**: Näyttää työhakemiston tilan ja paljastaa, että `README.md`-tiedostoa on muokattu mutta muutoksia ei ole vielä lisätty tai tallennettu.
* **git reset --hard**: Kumoaa kaikki tallentamattomat muutokset työhakemistosta ja palauttaa tiedostot edellisen commitin tilaan ilman peruutusmahdollisuutta.

## Tehtävä D

Tarkastelin varaston commit-historiaa ja tiedostoihin tehtyjä muutoksia komennolla `git log --patch`. Tulosteesta näkyi jokaisen commitin yksilöllinen tunniste (hash), tekijän nimi ja sähköposti, aikaleima, commit-viesti sekä tarkat rivikohtaiset muutokset (`+`-merkillä lisätyt rivit). Lopuksi tarkistin komennoilla `git config --global user.name` ja `git config --global user.email`, että omat käyttäjätietoni ovat oikein.

* **git log --patch**: Näyttää varaston commit-historian sekä jokaisen tallennuksen tarkat rivikohtaiset muutokset.
* **git config --global user.name** (ja **user.email**): Tulostaa Gitin globaalit käyttäjäasetukset ja varmistaa, että commitien tekijätiedot näkyvät oikein.

