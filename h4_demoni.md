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




## Tehtävät

### Laitteen tiedot

- AMD Ryzen 5 3600 6-Core Processor 3.59 GHz

- RAM: 16,0 Gt

- 64-bittinen käyttöjärjestelmä, x64-suoritin

- Windows 10 Pro, versio 22H2

  
