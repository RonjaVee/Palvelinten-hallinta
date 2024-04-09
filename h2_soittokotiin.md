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
- Orjan asennus (Ubuntu, Debian): ``sudo apt-get update`` ``sudo apt-get -y install salt-minion``
- Jokaisella orjalla oltava eri nimi, nimen voi antaa itse
- Orjan pitää tietää pääpalvelimen sijainti
- ``sudoedit /etc/salt/minion`` master: master-koneen ip id: minionin id (minionin id ei pakollinen) ``sudo systemctl restart salt-minion.service``
- Pääpalvelimelle annetaan orjan avain ``sudo salt-key -A``


Tiivistelmä Tero Karvisen ohjeesta Hello Salt Infra-as-Code. 3.4.2024. [https://terokarvinen.com/2024/hello-salt-infra-as-code/](https://terokarvinen.com/2024/hello-salt-infra-as-code/)

- Luodaan hello-moduuli ``mkdir -p /srv/salt/hello/`` -> ``cd /srv/salt/hello/``
- Moduuli voi olla esim. Apache -web-palvelin, tämä esimerkki simppeli demo
- /srv/salt/ -kansio näkyy kaikille orjille
- Varmista, että sijaintisi on /srv/salt/hello/, sitten ``sudoedit init.sls``
- Tiedostoon kirjoitetaan
    /tmp/hello:
    file.managed
- Testataan: ``salt-call --local state.apply hello``


## Tehtävät

### Laitteen tiedot

- AMD Ryzen 5 3600 6-Core Processor 3.59 GHz

- RAM: 16,0 Gt

- 64-bittinen käyttöjärjestelmä, x64-suoritin

- Windows 10 Pro, versio 22H2


Aloitus 9.4. klo 13:15.

__a.__ Lähdin etenemään Tero Karvisen [ohjeen](https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/?fromSearch=vagrant%20two%20machine) mukaan luomalla twohost-kansion ja sinne tekstitiedoston Vagrantfile. Koska työskentelin 
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

__b.__ Päätin tehdä a-kohdan t001-koneesta herran ja t002 orjan. Otin ssh-yhteyden t001-koneeseen, ja annoin komennot ``sudo apt-get update`` ja ``sudo apt-get -y install salt-master`` Karvisen [ohjeen](https://terokarvinen.com/2018/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/?fromSearch=salt%20quickstart) mukaan. Palomuuriin en koskenut, koska sitä ei ollut asennettu.

Sitten vaihdoin t002-koneelle ssh-yhteydellä, annoin komennot ``sudo apt-get update`` ja ``sudo apt-get -y install salt-minion``. Kertoakseni orjalle pääpalvelimen sijainnin, muokkasin tiedostoa ``sudoedit /etc/salt/minion``. 

![image](https://github.com/RonjaVee/Palvelinten-hallinta/assets/148786247/3863f452-36f2-4564-8e12-af0cc8bec1d9)


Sitten käynnistin koneen uudestaan, jotta asetukset tulisivat voimaan. ``sudo systemctl restart salt-minion.service``

Seuraavaksi palasin takaisin t001-koneelle ssh-yhteyden kautta ottaakseni sillä vastaan orjan avaimen. ``sudo salt-key -A`` Se ei toiminut, ja aloin tutkimaan syytä. Oletin, että IP-osoitteessa on vikaa, ja tarkistin pääpalvelimen IP-osoitteen komennolla 
``sudo salt-call --local network.ip_addrs``, ja IP-osoite olikin eri kuin esimerkissä, joten käytin sitä, käynnistin t002 uudelleen ja koetin uudestaan vastaanottaa avaimen t001-koneella. Vieläkin tuli sama ilmoitus.

![image](https://github.com/RonjaVee/Palvelinten-hallinta/assets/148786247/429c66e1-760e-4f88-a1b0-76f85b1041fd)

![image](https://github.com/RonjaVee/Palvelinten-hallinta/assets/148786247/41b336a2-3979-442c-9360-b0f7bf655ec9)

Tauko 15:00-17:20.

Aloitin homman alusta ``vagrant destroy`` ``vagrant up``. Suoritin saman ohjeen mukaan järjestyksessä kaikki komennot master- ja slave-koneilla. Jätin id:n pois hämäämästä. Vieläkään ei toiminut. Tarkistin molempien palvelimien tilat ja käynnistin molemmat uudelleen.

``sudo systemctl status salt-master`` ``sudo systemctl status salt-minion``

``sudo systemctl restart salt-minion`` ``sudo systemctl restart salt-master``

![image](https://github.com/RonjaVee/Palvelinten-hallinta/assets/148786247/3943513e-2b95-41ce-a24a-19099841048c)

Ei toiminut. Tarkistin ``sudo systemctl status salt-minion`` komennolla, mitä se näyttäisi (kysyin tässä kohtaa ChatGPT:ltä missä voisi olla vika, kun en saanut logeja auki (vagrant@t002:/var/log$ sudo cat /var/log/salt/minion.log
cat: /var/log/salt/minion.log: No such file or directory)).

![image](https://github.com/RonjaVee/Palvelinten-hallinta/assets/148786247/e32d2e81-d808-4297-8601-509f9d5d0329)

Masterilla ei näkynyt erroria. ``sudo systemctl status salt-master``

![image](https://github.com/RonjaVee/Palvelinten-hallinta/assets/148786247/c76dcc28-76fa-4944-8bb9-3ed7de99055b)

Kokeilinpa sitten masterin IP-osoitteen sijaan hostnamea t001. Ei toiminut. Sitten kokeilin IP-osoitetta 192.168.88.101. No, sehän sitten toimikin.

![image](https://github.com/RonjaVee/Palvelinten-hallinta/assets/148786247/ad1362a4-430b-4bcd-97fd-9b980d80e839)

__c.__ Kokeilin ohjeesta löytyviä esimerkkikomentoja ``sudo salt '*' cmd.run 'hostname -I'`` ja ``sudo salt '*' grains.item virtual``.

![image](https://github.com/RonjaVee/Palvelinten-hallinta/assets/148786247/a900b9cb-f30a-443a-bb17-3120bab0b9e9)

__d.__ Kokeilin idempotenttisia komentoja master-slave -yhteydellä:

    ``sudo salt '*' state.single pkg.installed name=cowsay``
    ``sudo salt '*' state.single file.managed /tmp/esimerkki``

Komennot loin yhdistelemällä aikaisemman raportin single.state-komentoja ja sudo salt '*'. Idempotenssia testasin suorittamalla jälkimmäisen komennon uudestaan -> no changes made.
    
![image](https://github.com/RonjaVee/Palvelinten-hallinta/assets/148786247/b85a5ad9-6f87-4d17-806e-f497d4a4976d)

![image](https://github.com/RonjaVee/Palvelinten-hallinta/assets/148786247/5e69c09a-dc80-4a08-9bbb-04872c9f44ff)

![image](https://github.com/RonjaVee/Palvelinten-hallinta/assets/148786247/f684786c-3082-4df1-9e43-dcc21e7c7f80)

__e.__ Aikaisemmin poiminkin grains.item virtual -komennolla tietoa. Kokeilin vielä ``sudo salt '*' grains.items|less`` komentoa. VirtualBoxhan siellä pohjalla on.

![image](https://github.com/RonjaVee/Palvelinten-hallinta/assets/148786247/af4d4e5c-b6fd-46b2-a4c2-aa5e72e713c2)

__f.__ Asensin master-koneelle micron ``sudo apt-get -y install micro``. Karvisen [ohjeen](https://terokarvinen.com/2024/hello-salt-infra-as-code/) mukaan lähdin toteuttamaan infraa koodina. Loin esimerkki-nimisen kansion ja siirryin sinne. Komennolla
``sudoedit init.sls`` kirjoitin tiedostoon /tmp/esim: file.managed.

![image](https://github.com/RonjaVee/Palvelinten-hallinta/assets/148786247/c2462116-4b56-41f2-8792-3237a968a53a)

![image](https://github.com/RonjaVee/Palvelinten-hallinta/assets/148786247/f8d8c6a4-8d20-4e8e-9e82-538180ecddab)

Suoritin komennon ``sudo salt '*' state.apply esimerkki`` toimeenpannakseni komennon, ja se onnistui. idempotenssi varmistui antamalla komento toiseen kertaan, no changes made.

![image](https://github.com/RonjaVee/Palvelinten-hallinta/assets/148786247/8c412e86-8b30-40b8-bd00-25676cd57c70)

![image](https://github.com/RonjaVee/Palvelinten-hallinta/assets/148786247/76a9d7b2-3caf-4cdd-9527-f92efbb63c3c)

Lopetus 18:35.

Päivitys 18:50 siistitty tiivistelmien komentoja ja esimerkkejä selkeämmäksi.

### Lähteet

Tehtävä: Karvinen, Tero. Palvelinten hallinta 2024 kurssisivu. [https://terokarvinen.com/2024/configuration-management-2024-spring/](https://terokarvinen.com/2024/configuration-management-2024-spring/)

Karvinen, Tero. Two Machine Virtual Network With Debian 11 Bullseye and Vagrant. 4.11.2021. [https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/?fromSearch=vagrant%20two%20machine](https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/?fromSearch=vagrant%20two%20machine)

Karvinen, Tero. Salt Quickstart – Salt Stack Master and Slave on Ubuntu Linux. 28.3.2018. [https://terokarvinen.com/2018/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/?fromSearch=salt%20quickstart](https://terokarvinen.com/2018/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/?fromSearch=salt%20quickstart)

Karvinen, Tero. Hello Salt Infra-as-Code. 3.4.2024. [https://terokarvinen.com/2024/hello-salt-infra-as-code/](https://terokarvinen.com/2024/hello-salt-infra-as-code/)

Karvinen, Tero. Run Salt Command Locally. 28.10.2021. [https://terokarvinen.com/2021/salt-run-command-locally/](https://terokarvinen.com/2021/salt-run-command-locally/)

OpenAI. "ChatGPT (GPT-3.5)". OpenAI API, [https://openai.com](https://openai.com), 2024.

