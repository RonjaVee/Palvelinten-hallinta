## Tiivistelmä

Karvinen, Tero. Salt Vagrant - automatically provision one master and two slaves. Kohdat Infra as Code - Your wishes as a text file ja top.sls - What Slave Runs What States. 28.3.2023. [https://terokarvinen.com/2023/salt-vagrant/#infra-as-code---your-wishes-as-a-text-file](https://terokarvinen.com/2023/salt-vagrant/#infra-as-code---your-wishes-as-a-text-file)

- Ensin luodaan kansio/moduuli salt state filelle: ``sudo mkdir -p /srv/salt/hello``
- Sitten luodaan salt state file tähän kansioon: ``sudoedit /srv/salt/hello/init.sls``
- init.sls kirjoitetaan seuraava teksti:
  
  ```
  /tmp/infra-as-code:
    file.managed
  ```

- Tila otetaan käyttöön komennolla ``sudo salt '*' state.apply hello``
- top.sls -tiedostolla määritellään, mitä tiloja mikäkin orja suorittaa
- ``sudo salt '*' state.apply hello^C``
- ``sudoedit /srv/salt/top.sls``

  ```
  base:
    '*':
      - hello
  ```

Salt contributors. Salt overview. Kohdat Rules of YAML, YAML simple structure, Lists and dictionaries - YAML block structures. [https://docs.saltproject.io/salt/user-guide/en/latest/topics/overview.html#rules-of-yaml](https://docs.saltproject.io/salt/user-guide/en/latest/topics/overview.html#rules-of-yaml). Luettu 23.4.2024.

- Salt state -tiedostoissa käytetään YAML-kieltä
- Data rakentuu avain-arvo -pareista; avain ja arvo erotetaan ``avain: arvo``
- YAML koostuu kolmesta perusrakenteesta: scalars, lists, dictionaries
- Scalars:
  ```
  avain1: arvo1
  avain2: arvo2
  avain3: arvo3
  ```
- Lists:

  ```
  yläavain1:
   - arvo1
   - arvo2
  yläavain2:
   - arvo3
   - arvo4
  ````
- Scalars:

```
yläavain1:
  avain1: arvo1
  avain2: arvo2
  avain3:
    - arvo3
    - arvo4
    - arvo5
```


Karvinen, Tero. Pkg-File-Service – Control Daemons with Salt – Change SSH Server Port. 3.4.2018. [https://terokarvinen.com/2018/04/03/pkg-file-service-control-daemons-with-salt-change-ssh-server-port/?fromSearch=karvinen%20salt%20ssh](https://terokarvinen.com/2018/04/03/pkg-file-service-control-daemons-with-salt-change-ssh-server-port/?fromSearch=karvinen%20salt%20ssh)

- SSH-palvelimen tila (asennus, hallinta, ylläpito) sshd.sls -tiedostossa
- sshd_config on SSH-palvelimen konfiguraatiotiedosto, jossa määritellään esim. portit, ja jota hallitaan Saltin avulla
- state.apply ottaa määritellyt tilat käyttöön
- Konfiguraatio testataan yhdistämällä SSH-palvelimeen yhdellä orjien koneista käyttäen määriteltyä porttia -> jos yhteys portin kautta saadaan, onnistui


## Tehtävät

### Laitteen tiedot

- AMD Ryzen 5 3600 6-Core Processor 3.59 GHz

- RAM: 16,0 Gt

- 64-bittinen käyttöjärjestelmä, x64-suoritin

- Windows 10 Pro, versio 22H2

Aloitus klo 16:15.

a. Hello SLS! 
Käynnistin aiemmin Vagrantilla luomani virtuaalikoneet t001 ja t002, joita hyödynnän näissä tehtävissä. Otin t001-koneeseen SSH-yhteyden ``vagrant ssh t001``. Käytin Karvisen [ohjetta](https://terokarvinen.com/2023/salt-vagrant/#infra-as-code---your-wishes-as-a-text-file) Hei maailma -tilan luomiseen.

![image](https://github.com/RonjaVee/Palvelinten-hallinta/assets/148786247/5db99ae6-beb6-418f-aceb-a3d6b76813ce)

![image](https://github.com/RonjaVee/Palvelinten-hallinta/assets/148786247/6a7443cb-32e0-4666-9078-f46c7b274d00)


b. Top. Loin edellisen tehtävän ohjeen mukaan top.sls -tiedoston /srv/salt -hakemistoon ja loin sinne listan, johon voi lisätä useita tiloja, jotka voi suorittaa yhtäaikaa yhdellä komennolla. Komento ``sudo salt '*' state.apply`` suorittaa kaikki tähän
tiedostoon listatut tilat.

![image](https://github.com/RonjaVee/Palvelinten-hallinta/assets/148786247/4356f31d-65d5-4c94-a1bd-8e71f20c0a94)

![image](https://github.com/RonjaVee/Palvelinten-hallinta/assets/148786247/f9d18df5-a53b-4b2b-9057-82b4de40bdb8)

c. Apache easy mode. Apachen asennuksen komennot:

- ``sudo apt-get update``
- ``sudo apt-get -y install apache2``
- ``sudoedit /etc/apache2/sites-available/esimerkki.com.conf``

```
<VirtualHost *:80>
 ServerName pyora.esimerkki.com
 ServerAlias www.esimerkki.com
 DocumentRoot /home/vagrant/publicsites/esimerkki.com
 <Directory /home/vagrant/publicsites/esimerkki.com>
   Require all granted
 </Directory>
</VirtualHost>
```

- ``sudo a2ensite esimerkki.com``
- ``sudo a2dissite 000-default.conf``
- ``sudo systemctl restart apache2``
- ``mkdir -p /home/vagrant/publicsites/esimerkki.com/``
- ``echo terve esimerkki > /home/vagrant/publicsites/esimerkki.com/index.html``
- ``curl localhost``

![image](https://github.com/RonjaVee/Palvelinten-hallinta/assets/148786247/39b3e3e5-c4c3-439f-9f44-0835e41b4122)




Lähteet

https://terokarvinen.com/2023/salt-vagrant/#infra-as-code---your-wishes-as-a-text-file

https://terokarvinen.com/2018/04/10/name-based-virtual-hosts-on-apache-multiple-websites-to-single-ip-address/

https://terokarvinen.com/2018/04/03/pkg-file-service-control-daemons-with-salt-change-ssh-server-port/?fromSearch=karvinen%20salt%20ssh
