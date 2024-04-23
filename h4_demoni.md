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

Huom. tästä eteenpäin lähtee sekoilu (kello oli n. 16:45).

Näistä komennoista loin salt-tilan: 

```
apache_install:
  pkg.installed:
    - name: apache2

apache_site_config:
  file.managed:
    - name: /etc/apache2/sites-available/esimerkki.com.conf
    - source: salt://etc/apache2/sites-available/esimerkki.com.conf

apache_enable_site:
  cmd.run:
    - name: a2ensite esimerkki.com
    - require:
      - file: apache_site_config

apache_disable_default_site:
  cmd.run:
    - name: a2dissite 000-default

apache_restart:
  service.running:
    - name: apache2
    - enable: True
    - require:
      - cmd: apache_disable_default_site

create_html_directory:
  file.directory:
    - name: /home/vagrant/publicsites/esimerkki.com/

create_index_html:
  file.managed:
    - name: /home/vagrant/publicsites/esimerkki.com/index.html
    - contents: "terve esimerkki\n"
    - require:
      - file: create_html_directory

curl_localhost:
  cmd.run:
    - name: curl localhost
    - unless: curl localhost
    - require:
      - service: apache_restart
```

Sitten loin tilalle kansion ``sudo mkdir /srv/salt/apache`` ja muokkasin init.sls -tiedostoa kuvan mukaisesti liittämällä sinne salt-tilan. Lisäsin tilan top.sls -tiedostoon.


![image](https://github.com/RonjaVee/Palvelinten-hallinta/assets/148786247/b506cbd8-11b2-47a1-927b-569ba0c393ba)

![image](https://github.com/RonjaVee/Palvelinten-hallinta/assets/148786247/06e44790-4d76-43dd-a485-41068c1acb9a)

Ei toiminut. Kokeilin sitten seuraavaa: 

```
apache_install:
  pkg.installed:
    - name: apache2

replace_default_index_html:
  file.managed:
    - name: /var/www/html/index.html
    - contents: "Tämä on uusi testisivu.\n"
    - user: www-data
    - group: www-data
    - mode: '0644'
    - require:
      - pkg: apache_install

apache_restart:
  service.running:
    - name: apache2
    - enable: True
    - require:
      - file: replace_default_index_html
```

Ei toiminut tämäkään. Virheilmoituksessa tuli ainakin seuraavaa:      ID: apache_install
    Function: pkg.installed
        Name: apache2
      Result: False
     Comment: An error was encountered while installing package(s): E: Release file for https://security.debian.org/debian-security/dists/bullseye-security/InRelease is not valid yet (invalid for another 5d 12h 18min 33s). Updates for this repository will not be applied.


Päätin luoda uudet koneet Vagrantilla ja kokeilla koko hommaa uudestaan. ``mkdir esimerkkikone`` ``cd .\esimerkkikone\`` ``notepad Vagrantfile``
Tiedostoon loin kolme Debian-konetta (machine1, machine2, machine3) ChatGPT:n antaman konfiguraation mukaan.

``vagrant up``

Koneiden luomisessa meni muutama minuutti ja toisesta huoneesta kuului "kuka siin netis on" -huutelua.
Huomasin, että luodut koneet olivat Debian10 (Buster) eli vanhempaa mallia kuin Debian11 (Bullseye). Poistin nämä vanhat koneet, mutta en enää kehdannut laittaa uusia pystyyn. Tälläistä konfiguraatiota on tarkoitus käyttää niille:

```
Vagrant.configure("2") do |config|

  # Configuration for machine1
  config.vm.define "machine1" do |machine1|
    machine1.vm.box = "debian/bullseye64"
    machine1.vm.network "private_network", ip: "192.168.50.101"
    # Add any additional configuration for machine1
  end

  # Configuration for machine2
  config.vm.define "machine2" do |machine2|
    machine2.vm.box = "debian/bullseye64"
    machine2.vm.network "private_network", ip: "192.168.50.102"
    # Add any additional configuration for machine2
  end

  # Configuration for machine3
  config.vm.define "machine3" do |machine3|
    machine3.vm.box = "debian/bullseye64"
    machine3.vm.network "private_network", ip: "192.168.50.103"
    # Add any additional configuration for machine3
  end

end
```
Homma jäi nyt valitettavasti kesken. Lopetus klo 18:00.

### Lähteet

Tehtävänanto: Infra as Code - Palvelinten hallinta 2024 [https://terokarvinen.com/2024/configuration-management-2024-spring/](https://terokarvinen.com/2024/configuration-management-2024-spring/)

Karvinen, Tero. Salt Vagrant - automatically provision one master and two slaves. 28.3.2023. [https://terokarvinen.com/2023/salt-vagrant/#infra-as-code---your-wishes-as-a-text-file](https://terokarvinen.com/2023/salt-vagrant/#infra-as-code---your-wishes-as-a-text-file)

Karvinen, Tero. Name Based Virtual Hosts on Apache – Multiple Websites to Single IP Address. 10.4.2018. [https://terokarvinen.com/2018/04/10/name-based-virtual-hosts-on-apache-multiple-websites-to-single-ip-address/](https://terokarvinen.com/2018/04/10/name-based-virtual-hosts-on-apache-multiple-websites-to-single-ip-address/)

Karvinen, Tero. Pkg-File-Service – Control Daemons with Salt – Change SSH Server Port. 3.4.2018. [https://terokarvinen.com/2018/04/03/pkg-file-service-control-daemons-with-salt-change-ssh-server-port/](https://terokarvinen.com/2018/04/03/pkg-file-service-control-daemons-with-salt-change-ssh-server-port/)

Karvinen, Tero. Run Salt Command Locally. 4.11.2021. [https://terokarvinen.com/2021/salt-run-command-locally/](https://terokarvinen.com/2021/salt-run-command-locally/)

Karvinen, Tero. Two Machine Virtual Network With Debian 11 Bullseye and Vagrant. 4.11.2021. [https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/](https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/)

Salt contributors. Salt overview. Kohdat Rules of YAML, YAML simple structure, Lists and dictionaries - YAML block structures. [https://docs.saltproject.io/salt/user-guide/en/latest/topics/overview.html#rules-of-yaml](https://docs.saltproject.io/salt/user-guide/en/latest/topics/overview.html#rules-of-yaml). Luettu 23.4.2024.

OpenAI. "ChatGPT (GPT-3.5)". OpenAI API. 2024 [https://openai.com](https://openai.com)
