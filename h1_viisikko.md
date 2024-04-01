## Tiivistelmät

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





## Tehtävät

### Laitteen tiedot

- AMD Ryzen 5 3600 6-Core Processor 3.59 GHz

- RAM: 16,0 Gt

- 64-bittinen käyttöjärjestelmä, x64-suoritin

- Windows 10 Pro, versio 22H2

  
Aloitus 17:15.


Saltin asennus: asensin Saltin Windowsille sivustolta (vain yksi latauslinkki Windowsille) [https://docs.saltproject.io/salt/install-guide/en/latest/topics/install-by-operating-system/windows.html#windows-downloads](https://docs.saltproject.io/salt/install-guide/en/latest/topics/install-by-operating-system/windows.html#windows-downloads). Suoritin asennuksen, ja tarkasin ``salt-call --version`` komennolla, että asennus oli onnistunut.

![image](https://github.com/RonjaVee/Palvelinten-hallinta/assets/148786247/f96f29a9-d80e-46d2-8641-f35732a594c5)


Vagrantin asennus: asensin Vagrantin Windowsille sivustolta (latauslinkki Windows AMD64 version 2.4.1) [https://developer.hashicorp.com/vagrant/install?product_intent=vagrant](https://developer.hashicorp.com/vagrant/install?product_intent=vagrant). Annoin sitten komennon Karvisen [ohjeen](https://terokarvinen.com/2017/vagrant-revisited-install-boot-new-virtual-machine-in-31-seconds/) mukaan: ``vagrant init bento/ubuntu-16.04`` ja loin virtuaalikoneen komennolla ``vagrant up``. Virtuaalikone näkyi Virtualboxissa.

![image](https://github.com/RonjaVee/Palvelinten-hallinta/assets/148786247/16e88167-8b11-4a25-b804-89eb53785031)
![image](https://github.com/RonjaVee/Palvelinten-hallinta/assets/148786247/208aa910-608e-41bc-9649-ff5e47dfefdf)

