## Tiivistelmä

Tiivistelmä Tero Karvisen ohjeesta Two Machine Virtual Network With Debian 11 Bullseye and Vagrant. 4.11.2021. [https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/?fromSearch=vagrant%20two%20machine](https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/?fromSearch=vagrant%20two%20machine)

- Vagrant ja Virtualbox tulee olla asennettuna
- Luodaan kansio projektille
- Kansioon luodaan Vagrantfile, johon konfiguroidaan palvelimet
- Konfiguraation jälkeen virtuaalikoneisiin voi ottaa ssh-yhteyden
- ``Vagrant destroy`` -komennolla voi tuhota virtuaalikoneet
- ``Vagrant up`` -komenolla voi sen jälkeen avata uudet koneet

Tiivistelmä Tero Karvisen ohjeesta Salt Quickstart – Salt Stack Master and Slave on Ubuntu Linux. 28.3.2018. [https://terokarvinen.com/2018/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/?fromSearch=salt%20quickstart](https://terokarvinen.com/2018/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/?fromSearch=salt%20quickstart)

- Orjat voivat olla missä vaan, herran tulee olla julkisessa verkossa ja orjien tulee tietää sen osoite, jotta herra voi hallita orjia
- Masterin, herran, pääpalvelimen, mitä nimeä siitä käyttääkään
- Pääpalvelimen palomuurissa tulee olla portit 4505/tcp ja 4506/tcp auki
- Orjan asennus (Ubuntu, Debian): ``slave$ sudo apt-get update`` ``slave$ sudo apt-get -y install salt-minion``
- Jokaisella orjalla oltava eri nimi, nimen voi antaa itse
- Orjan pitää tietää pääpalvelimen sijainti
- ``slave$ sudoedit /etc/salt/minion`` master: 10.0.0.88 id: id ``slave$ sudo systemctl restart salt-minion.service``
- Pääpalvelimelle annetaan orjan avain ``master$ sudo salt-key -A``


Tiivistelmä Tero Karvisen ohjeesta Hello Salt Infra-as-Code. 3.4.2024. [https://terokarvinen.com/2024/hello-salt-infra-as-code/](https://terokarvinen.com/2024/hello-salt-infra-as-code/)

- Asennetaan salt minion
- Luodaan hello-moduuli ``mkdir -p /srv/salt/hello/`` -> ``cd /srv/salt/hello/``
- Moduuli voi olla esim. Apache -web-palvelin
- /srv/salt/ -kansio näkyy kaikille orjille
- Varmista, että sijaintisi on /srv/salt/hello/, sitten ``sudoedit init.sls``
- Tiedostoon kirjoitetaan
    /tmp/helloronja:
    file.managed
- Testataan: ``salt-call --local state.apply hello``


## Tehtävät

### Laitteen tiedot

- AMD Ryzen 5 3600 6-Core Processor 3.59 GHz

- RAM: 16,0 Gt

- 64-bittinen käyttöjärjestelmä, x64-suoritin

- Windows 10 Pro, versio 22H2


Aloitus 9.4. klo 13:15.

a. Lähdin etenemään Tero Karvisen [ohjeen](https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/?fromSearch=vagrant%20two%20machine) mukaan luomalla twohost-kansion ja sinne tekstitiedoston Vagrantfile. Koska työskentelin 
Windows-ympäristössä, en keksinyt heti, millä editorilla voisin helpoiten tekstitiedoston luoda, joten kysyin sitä ChatGPT:ltä, ja notepad vaikutti simppeleimmältä ratkaisulta.

``mkdir twohost/`` ``cd twohost/`` ``notepad Vagrantfile``

Muokkasin tiedostoa ohjeen mukaan, editorina käytin notepadia ja tallensin tiedoston tekstitiedostona twohost-kansioon.

![image](https://github.com/RonjaVee/Palvelinten-hallinta/assets/148786247/9d98c2b6-62ed-4359-bd5d-837f34465038)

![image](https://github.com/RonjaVee/Palvelinten-hallinta/assets/148786247/2de9b555-7d54-49d7-8804-f6884bb9b753)

SSH-komento ei kuitenkaan toiminut, ja alkoi epätoivo iskeä. Luomassani Vagrantfilessä oli vikaa. 

![image](https://github.com/RonjaVee/Palvelinten-hallinta/assets/148786247/92a490dc-232f-4174-8f4f-e0a417c97c3f)

Kokeilin erilaisia Vagrant-komentoja, ja avasin kansion Resurssienhallinnan kautta. Huomasin, että ``vagrant init`` -komento loi kansioon samannimisen Vagrantfilen, ja keksin muokata sitä avaamalla sen notepadissa ja liittämällä sinne ohjeen mukaisen pätkän
Ruby-koodia. Sitten annoin ``vagrant ssh t001`` -komennon, mutta vielä ennen sitä piti tietenkin laittaa virtuaalikone päälle ``vagrant up`` -komennolla. Virtualbox kysyi joitakin lupia koneen käynnistyessä. Komentokehotteessa tapahtui pitkään asioita t001 ja t002
koskien ja aikaa kului ehkä minuutin verran, kunnes virtuaalikone oli käynnistetty.

![image](https://github.com/RonjaVee/Palvelinten-hallinta/assets/148786247/9c05add3-4b3d-4b7b-950d-ccb7af017896)


Sitten otin ssh-yhteyden t001-koneeseen, ja pääsin sisälle. Suoritin pingauksen t002-koneeseen ``ping -c 1 192.168.88.102``, ja sain vastauksen. Tein saman toisin päin, ja paketit liikkuivat kuten pitää.

![image](https://github.com/RonjaVee/Palvelinten-hallinta/assets/148786247/853222f7-c0cf-47ec-8f18-86694e2d5657)

![image](https://github.com/RonjaVee/Palvelinten-hallinta/assets/148786247/8d661704-17fe-4b75-be80-2d23b3c997e3)


