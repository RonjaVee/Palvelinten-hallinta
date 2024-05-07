## Tiivistelmä

Tiivistelmä tekstistä Windows Package Manager. Salt Project. Generoitu 30.4.2024. [https://docs.saltproject.io/en/latest/topics/windows/windows-package-manager.html](https://docs.saltproject.io/en/latest/topics/windows/windows-package-manager.html)

- Windowsiin voi asentaa paketteja Saltilla käyttämällä .sls-tiedostoa
- Yleisimpiä paketteja saadaan SaltStack-repositoriosta Githubista [https://github.com/saltstack/salt-winrepo-ng](https://github.com/saltstack/salt-winrepo-ng)
- Kirjastojen asennus (valinnainen): GitPython tai pygit2
- Paikallinen Git-repositorio täytetään salt-winrepo-ng:llä: ``salt-run winrepo.update_git_repos`` (masterilla) tai ``salt-call --local winrepo.update_git_repos`` (minion ilman masteria)
- Minionin tietokanta päivitetään: ``salt -G 'os:windows' pkg.refresh_db`` (masterilla) tai ``salt-call --local pkg.refresh_db`` (minion ilman masteria)
- Paketit asennetaan: ``salt * pkg.install 'paketin_nimi'`` (masterilla) tai ``salt-call --local pkg.install "paketin_nimi"`` (minion ilman masteria)
- Paketit ja niiden versiot voidaan listata komennolla ``salt -G 'os:windows' pkg.list_pkgs`` (masterilla) tai ``salt-call --local pkg.list_pkgs`` (minion ilman masteria)
- ``salt winminion pkg.list_available paketin_nimi`` (masterilla) tai ``salt-call --local pkg.list_available paketin_nimi`` (minion ilman masteria) listaa saatavilla olevat versiot paketista


## Tehtävät

### Laitteen tiedot

- AMD Ryzen 5 3600 6-Core Processor 3.59 GHz
- RAM: 16,0 Gt
- 64-bittinen käyttöjärjestelmä, x64-suoritin
- Windows 10 Pro, versio 22H2


Aloitus 13:15.

a. Paketti Windowsia. Noudatin tässä tekemääni tiivistelmää. Aloitin kloonaamalla salt-winrepo-ng:n ``git clone git@github.com:saltstack/salt-winrepo-ng.git``. Täytin paikallisen Git-reposition ``salt-call --local winrepo.update_git_repos``. 
![image](https://github.com/RonjaVee/Palvelinten-hallinta/assets/148786247/7d20b650-0bb5-4b96-bb29-1626ec1f8d17)

Sitten päivitin minionin tietokannan ``salt-call --local pkg.refresh_db``.

![image](https://github.com/RonjaVee/Palvelinten-hallinta/assets/148786247/faee5630-6c96-4797-ae6b-d59390056c53)

Sitten paketin asennus. Päätin asentaa curlin, mutta komento ``salt-call --local pkg.install "curl"`` ei toiminut. Kokeilin komentoa ``salt-call --local pkg.list_available curl``, ja komento listasi
saatavilla olevat versiot. 

![image](https://github.com/RonjaVee/Palvelinten-hallinta/assets/148786247/5f08ad49-715c-45a8-a338-bcb120648cdc)

Kokeilin sitten ohjeessa ollutta esimerkkiä ``salt-call --local pkg.install "firefox_x64"```.

![image](https://github.com/RonjaVee/Palvelinten-hallinta/assets/148786247/332999b7-6a99-44b2-b391-623f91839e2c)

Kokeilin sitten poistaa Firefoxin ja asentaa uudelleen, ja ymmärtääkseni se onnistui? Olen hiukan hämmentynyt, en tiedä, missä mättää.

![image](https://github.com/RonjaVee/Palvelinten-hallinta/assets/148786247/7ba36e9f-7792-4e0e-8adf-859ca770a3fa)


b. Benchmark. 

Projekti 1. [https://ottohanninen.wordpress.com/2021/05/19/configuration-management-systems-palvelinten-hallinta-spring-2021-h7-oma-moduli/](https://ottohanninen.wordpress.com/2021/05/19/configuration-management-systems-palvelinten-hallinta-spring-2021-h7-oma-moduli/) Tiedostot: [https://github.com/ottohan/LAMP](https://github.com/ottohan/LAMP) Lisenssi: GNU General Public License v3.0, avoimen lähdekoodin lisenssi, joka on suunniteltu edistämään avoimen lähdekoodin ohjelmistojen kehittämistä ja jakamista sekä suojaamaan ohjelmistojen vapautta ja avoimuutta. Lisenssi ilmoitettu Github-repositoriossa. Tekijä: Otto Hänninen. Vuosi: 2021. Aikaisemman kurssin oma moduli -tehtävä, joka asentaa SSH:n, tekee sopivat reijät palomuuriin, asentaa Apachen ja korvaa default-kotisivun ja asentaa Mariadb:n, elaatiotietokannan hallintajärjestelmän sekä PHP-laajennuksen. PHP-kieltä käytetään yleisesti web-kehityksessä. Asennukset Saltilla, alustana käytetty Xubuntua. Tämä moduli antaa hyvän aloituksen ja perusvälineet web-sovelluskehitykselle, voisin hyödyntää sitä itsekin.

Projekti 2. [https://github.com/clinta/salt-pwgen](https://github.com/clinta/salt-pwgen). Lisenssi: BSD-2-Clause license, avoimen lähdekoodin lisenssi. Eroaa GNU v.3.0 siten, että se ei rajoita jatkokäyttöä yhtä
paljon: jatkokäytössä voi käyttää suljetun tai avoimen lähdekoodin lisenssiä, kun taas GNU v.3.0 vaatii, että johdannaisteoksissakin käytetään samaa lisenssiä, jotta ne jäävät avoimen lähdekoodin alaisiksi. Lisenssi ilmoitettu Github-repositoriossa. Tekijä: Clint Armstrong. Vuosi: 2015. Tämä Salt-moduli antaa mahdollistaa salasanojen luomis- ja tallennusprosessin automatisoinnin Saltin avulla. Se hyödyntää pass-ohjelmaa, salasanojen hallintatyökalua Unix-järjestelmissä. Toimii POSIX-standardin mukaisissa järjestelmissä (Unix-pohjaiset käyttöjärjestelmät, esim. Linux ja MacOS). Salasanojen hallintajärjestelmillä voidaan parantaa tietoturvaa, kun salasanat on generoitu satunnaisesti ja ne vaihtuvat määritellyin väliajoin.

Projekti 3. [https://github.com/sawulohi/h7] Lisenssi: GNU General Public License v3.0. Lisenssi ilmoitettu Github-repositoriossa. Tekijä: sawulohi. Vuosi: 2022. Tämäkin aikaisemman kurssin oma moduli -tehtävä. Asentaa paketit gimp, git, micro, vlc ja Firefoxille darkmoden. Simppeli host-koneen aloitussetti sisältäen kuvanmuokkausohjelman, tekstieditorin, mediaplayerin ja gitin. Moduli on tehty Debian-koneelle, jossa on valmiina Firefox.

c. Testbench. Virtuaalikoneissa ilmeni vikaa, enkä enää kerkeä psytyttämään uusia. Olisin kloonannut projekti 3. repositorion /srv/salt-hakemistoon ja antanut komennon ``sudo salt '*' state.apply``.


d. Viisi ideaa. 

1. Salasanojen hallinta: salasanojen generointi, tallentaminen ja jakaminen eri järjestelmiin ja palveluihin.Tässä voisi integroida suosittuja salasanojen hallintajärjestelmiä tai tarjota oman hallintaratkaisun. Tietoturva kiinnostaa, joten haluaisin tutustua salasanojen hallintajärjestelmiin.

2. Käyttäjien hallinta: Salasanoille olisi hyvä luoda käyttäjiäkin, jotta niitä pääsee kokeilemaan. Niiden oikeuksiakin voi sitten säädellä ehkä myös.

3. Ohjelmistojen asennus ja päivitys: joitakin paketteja olisi kiva asentaa, sellaiset peruspaketit, joita tarvitsee usein.

4. Dark modea päälle: aikaisemman tehtävän projekti 3. oli laitettu Firefoxille tumma tila päälle. Käytän itse dark modea aina kun mahdollista, niin tätä haluaisin kokeilla omassa tehtävässäni.

5. Jotain muuta, erilaista?: Minecraft-palvelimen pystyttäminen virtuaalikoneelle siten, että sillä voisi pelata (edes kotiverkossa) olisi hauskaa. En tiedä yhtään, kuinka monimutkaiseksi tehtävä tulisi, mutta tälläinen konkreettinen idea tuli mieleen. Ei tarvitsisi sitten käyttää maksullista palvelinta.


Lopetus klo 16:10.

### Lähteet

Tehtävä: Karvinen, Tero. Palvelinten hallinta 2024 kurssisivu. [https://terokarvinen.com/2024/configuration-management-2024-spring/#h6-benchmark](https://terokarvinen.com/2024/configuration-management-2024-spring/#h6-benchmark)

Hänninen, Otto. Configuration Management Systems – Palvelinten Hallinta – Spring 2021 – h7 Oma moduli. 19.5.2021. [https://ottohanninen.wordpress.com/2021/05/19/configuration-management-systems-palvelinten-hallinta-spring-2021-h7-oma-moduli/](https://ottohanninen.wordpress.com/2021/05/19/configuration-management-systems-palvelinten-hallinta-spring-2021-h7-oma-moduli/)

Armstrong, Clint. Salt-pwgen. Päivitetty 24.9.2019. [https://github.com/clinta/salt-pwgen](https://github.com/clinta/salt-pwgen)

Wikipedia. LAMP (software bundle). Päivitetty 11.4.2024. [https://en.wikipedia.org/wiki/LAMP_(software_bundle)](https://en.wikipedia.org/wiki/LAMP_(software_bundle))

Wikipedia. BSD licenses. Päivitetty 29.3.2024. [https://en.wikipedia.org/wiki/BSD_licenses](https://en.wikipedia.org/wiki/BSD_licenses)

Sawulohi. h7 Mini module for a new desktop environment using SaltStack. Päivitetty 15.12.2022. https://github.com/sawulohi/h7


