## x. Tiivistelmät

[Karivnen, Tero. Raportin kirjoittaminen. 4.6.2006. https://terokarvinen.com/2006/06/04/raportin-kirjoittaminen-4/](https://terokarvinen.com/2006/06/04/raportin-kirjoittaminen-4/)

- Raportin ohjeiden on oltava toistettavia toisen henkilön toimesta samassa ympäristössä
- Raportista on nähtävä täsmällisesti mitä tehtiin, mitä tapahtui ja milloin tarkkoine vikailmoituksineen
- Raportissa on käytettävä korrektia kieltä ja aikamuotoa ja sen rakenne tulee olla helposti seurattava
- Raportissa tulee viitata käytettyihin lähteisiin
- Plagiointi, sepittäminen sekä tekijänoikeuksien rikkominen on kiellettyä

[Karivnen, Tero. Create a Web Page Using Github. 28.3.2023. https://terokarvinen.com/2023/create-a-web-page-using-github/](https://terokarvinen.com/2023/create-a-web-page-using-github/)

- Kirjaudu Githubiin
- Luo uusi repositorio
- Luo repositoriolle luomisvaiheessa README.md -tiedosto ja valitse lisenssi
- Repositorioon luodaan uusi .md-tiedosto -> commit
- Nyt voit jakaa uuden Github-sivusi kopioimalla luodun sivun osoitteen

[Karvinen, Tero. Run Salt Command Locally. 28.10.2021. https://terokarvinen.com/2021/salt-run-command-locally/](https://terokarvinen.com/2021/salt-run-command-locally/)

- Saltin asennus (Debian/Ubuntu): ``sudo apt-get update`` ``sudo apt-get -y install salt-minion``
- pkg, file, service, user, cmd ovat tärkeimpiä Saltin tilafunktioita
- Ohjeet komennolla ``sudo salt-call --local sys.state_doc``



## Tehtävät

### Laitteen tiedot

- AMD Ryzen 5 3600 6-Core Processor 3.59 GHz

- RAM: 16,0 Gt

- 64-bittinen käyttöjärjestelmä, x64-suoritin

- Windows 10 Pro, versio 22H2

  
Aloitus 17:15.


a. Saltin asennus: asensin Saltin Windowsille sivustolta (vain yksi latauslinkki Windowsille) [https://docs.saltproject.io/salt/install-guide/en/latest/topics/install-by-operating-system/windows.html#windows-downloads](https://docs.saltproject.io/salt/install-guide/en/latest/topics/install-by-operating-system/windows.html#windows-downloads). Suoritin asennuksen, ja tarkasin ``salt-call --version`` komennolla, että asennus oli onnistunut.

![image](https://github.com/RonjaVee/Palvelinten-hallinta/assets/148786247/f96f29a9-d80e-46d2-8641-f35732a594c5)


b. ja c. Vagrantin asennus: asensin Vagrantin Windowsille sivustolta (latauslinkki Windows AMD64 version 2.4.1) [https://developer.hashicorp.com/vagrant/install?product_intent=vagrant](https://developer.hashicorp.com/vagrant/install?product_intent=vagrant). Annoin sitten komennon Karvisen [ohjeen](https://terokarvinen.com/2017/vagrant-revisited-install-boot-new-virtual-machine-in-31-seconds/) mukaan: ``vagrant init bento/ubuntu-16.04`` ja loin virtuaalikoneen komennolla ``vagrant up``. Virtuaalikone näkyi Virtualboxissa.

![image](https://github.com/RonjaVee/Palvelinten-hallinta/assets/148786247/16e88167-8b11-4a25-b804-89eb53785031)
![image](https://github.com/RonjaVee/Palvelinten-hallinta/assets/148786247/208aa910-608e-41bc-9649-ff5e47dfefdf)

a. Otin sitten ssh-yhteyden Windows-koneeltani Vagrantilla luomaani virtuaalikoneeseen komennolla ``vagrant ssh`` ja lähdin asentamaan sille Saltia.
``sudo apt-get update``
``sudo apt-get install salt-minion``

Tarkistin, että asennus onnistui ``sudo salt-call --version``

![image](https://github.com/RonjaVee/Palvelinten-hallinta/assets/148786247/0475659b-ee20-4e7c-9718-91d15d5b2b77)

b. Sitten kokeilin viisi tärkeintä Saltin tilafunktiota antamalla seuraavat komennot seuraavin tuloksin:

- Pakettien hallintaa
  ``sudo salt-call --local -l info state.single pkg.installed tree``
  Tällä komennolla tarkastettiin tree-nimisen paketin tila, ja jos sitä ei ole asennettu, Salt koettaa sen asentaa. 

![image](https://github.com/RonjaVee/Palvelinten-hallinta/assets/148786247/87a75679-ad6a-4e09-8b0f-2171b4900a71)

- Tiedostojen hallintaa
  ``sudo salt-call --local -l info state.single file.managed /tmp/hello``
  Tällä komennolla luodaan tiedosto hello.
  
![image](https://github.com/RonjaVee/Palvelinten-hallinta/assets/148786247/99111b73-3685-40b7-a5fb-41be46283603)


- Apache-palvelimen käynnistys(?). Sitä minulla ei ole asennettuna Windowsille.
  ``sudo salt-call --local -l info state.single service.running apache2 enable=True``
    Koska minulla ei ole Apachea asennettuna, on result false.

![image](https://github.com/RonjaVee/Palvelinten-hallinta/assets/148786247/b4f0ada2-b328-4ae6-a815-6f31aef015a7)

- Uuden käyttäjän luominen
  ``sudo salt-call --local -l info state.single user.present ronjav``

![image](https://github.com/RonjaVee/Palvelinten-hallinta/assets/148786247/08c4232c-9e15-4484-9bf7-1fc7344c74d1)

- Touch-komento
  ``sudo salt-call --local -l info state.single cmd.run 'touch /tmp/foo' creates="/tmp/foo"``

![image](https://github.com/RonjaVee/Palvelinten-hallinta/assets/148786247/6b765494-c62b-4549-ae95-7cd9a5be4c3a)

 Klo 18:25 täytyi lopettaa.

 3.4.2024, 16:00.

c. Komennolla ``sudo salt-call --local state.single file.managed /tmp/testfile content="Hello, world!"`` loin tiedoston testfile, johon kirjoitin "Hello world!". Kun toistin saman komennon, mikään ei muuttunut, sillä 
Salt tunnisti, että komento oli jo kerran suoritettu, ja luotu tiedosto olemassa samalla sisällöllä. Kun tiedostoa muokataan komennolla, sen tila muuttuu, esim. poistamalla tiedoston.
``sudo salt-call --local -l info state.single file.absent /tmp/testfile``

![image](https://github.com/RonjaVee/Palvelinten-hallinta/assets/148786247/32a4c52a-2348-4be3-87ad-7830592b76b4)

![image](https://github.com/RonjaVee/Palvelinten-hallinta/assets/148786247/a22a259a-5388-4a05-90a1-e12718d3221b)

![image](https://github.com/RonjaVee/Palvelinten-hallinta/assets/148786247/7a892869-c736-4d3b-ae1d-1dc33582e506)

Idempotenssilla varmistetaan, että komentosarjoja voidaan toistaa ilman ei-haluttuja muutoksia. Salt hyödyntää idempotenttista periaatetta, mikä on hyödyllistä virheiden ehkäisemiseksi suurempien järjestelmien hallinnassa.

d. En saanut komentoa toimimaan. Tuli error- ja warning-viestejä. WARNING: CONFIG 'C:\ProgramData\Salt Project\Salt\conf' directory does not exist.
Lopetus 16:30.

Lisäys 23.4.2024: Syy d-kohdan epäonnistumiseen johtui siitä, etten avannut Powershelliä administratorina. Tällaista tietoa irtosi komennolla ``salt-call --local grains.items`` (pitkä lista jatkui):

![image](https://github.com/RonjaVee/Palvelinten-hallinta/assets/148786247/197d5137-81d9-40f4-b46a-017f70d3e824)


### Lähteet

Karvinen, Tero. Palvelinten hallinta 2024 kurssisivu. [https://terokarvinen.com/2024/configuration-management-2024-spring/](https://terokarvinen.com/2024/configuration-management-2024-spring/)

Karvinen, Tero. Run Salt Command Locally. 28.10.2021. [https://terokarvinen.com/2021/salt-run-command-locally/](https://terokarvinen.com/2021/salt-run-command-locally/)

Karvinen, Tero. Vagrant Revisited - Install & Boot New Virtual Machine in 31 seconds. 11.4.2017. [https://terokarvinen.com/2017/vagrant-revisited-install-boot-new-virtual-machine-in-31-seconds/](https://terokarvinen.com/2017/vagrant-revisited-install-boot-new-virtual-machine-in-31-seconds/)

Idempotenssi. Wikipedia, The Free Encyclopedia. Wikimedia Foundation, Inc. 3.7.2019. [https://fi.wikipedia.org/wiki/Idempotenssi](https://fi.wikipedia.org/wiki/Idempotenssi)









