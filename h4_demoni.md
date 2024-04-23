## Tiivistelmä

Karvinen, Tero. Salt Vagrant - automatically provision one master and two slaves. Kohdat Infra as Code - Your wishes as a text file ja top.sls - What Slave Runs What States. 28.3.2023.

- Ensin luodaan kansio salt state filelle: ``sudo mkdir -p /srv/salt/hello``
- Sitten luodaan salt state file tähän kansioon: ``sudoedit /srv/salt/hello/init.sls``
- init.sls kirjoitetaan seuraava teksti:
  
  ```
  /tmp/infra-as-code:
    file.managed
  ```

- Tila otetaan käyttöön komennolla ``sudo salt '*' state.apply hello``





## Tehtävät

### Laitteen tiedot

- AMD Ryzen 5 3600 6-Core Processor 3.59 GHz

- RAM: 16,0 Gt

- 64-bittinen käyttöjärjestelmä, x64-suoritin

- Windows 10 Pro, versio 22H2

  
