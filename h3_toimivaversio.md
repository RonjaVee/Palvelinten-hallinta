## Tiivistelmät

Tiivistelmä kirjasta Chacon and Straub 2014: Pro Git, 2. painos, kohdasta [1.3 Getting Started - What is Git?](https://git-scm.com/book/en/v2/Getting-Started-What-is-Git%3F)

- Git on versionhallintajärjestelmä, jonka avulla saman projektin parissa voi työskennellä useampi taho
- Aikaisempaan versioon voi tarvittaessa palata tai sitä voi tarkastella
- Suurin osa toiminnoista tapahtuu paikallisesti, jolloin tarve verkkoon pääsylle vähenee
- Datan häviäminen tai korruptoituminen ei ole mahdollista Gitin huomaamatta sen tarkastusmekanismin ansiosta
- Git ei muuta dataa, vaan lisää vanhan päälle lähes kaikissa tilanteissa


[Prajapati, Amit. What is git commit, push, pull, log, aliases, fetch, config & clone. Medium 20.9.2019.](https://medium.com/mindorks/what-is-git-commit-push-pull-log-aliases-fetch-config-clone-56bc52a3601c)

- Git add: muutetut tiedostot siirtyvät staging-alueelle, jossa Git tarkastaa ja tallentaa muutokset
- Git commit: tehdyt muutokset siirtyvät staging-alueelta paikalliseen repositorioon, muutokset tallentuvat pysyvästi versionhallintaan
- Git pull: etärepositorioon (esim. Github) tehdyt muutokset tallentuvat paikalliseen repositorioon
- Git push: paikalliseen repositorioon tallennetut muutokset siirretään etärepositorioon


Varaston terokarvinen/suolax/ historia [(https://github.com/terokarvinen/suolax)](https://github.com/terokarvinen/suolax), eli mitä muutoksia sinne on tehty (commit messages):

- Improve usage instructions
- Clean up README.md
- Run Salt states from version controlled repository




## Tehtävät

### Laitteen tiedot

- AMD Ryzen 5 3600 6-Core Processor 3.59 GHz

- RAM: 16,0 Gt

- 64-bittinen käyttöjärjestelmä, x64-suoritin

- Windows 10 Pro, versio 22H2



Aloitus ko 16:50.

a. Online

Loin Githubiin uuden repositorion nimeltä h3summer.

![image](https://github.com/RonjaVee/Palvelinten-hallinta/assets/148786247/e7c5e7c0-02b6-4def-8d83-06d0237e0ff8)

b. Dolly

Lähdin kloonaamaan repositoriota kopioimalla Githubista saatavan SSH-linkin. SSH-avaimen olin jo aiemmin luonut Githubiin, joten sitä ei tarvinnut tehdä uudestaan.

![image](https://github.com/RonjaVee/Palvelinten-hallinta/assets/148786247/8fb5f06e-1fa3-4e5e-b87d-323d47aba737)

``git clone git@github.com:RonjaVee/h3summer.git``

Siirryin hakemistoon ``cd h3summer``. ``git config --global user.name "Ronja Vauhkonen"`` ja tein muutoksia README.md-tiedostoon ``notepad README.md``. En tosin tarkastanut ennen nimen muokkausta, oliko se jo 
alunperin oikein, jolloin nimi ei muutu.

Annoin komennot ``git add .`` ja sitten ``git commit``. Commit-viestin editori oli kuitenkin minulle täysin mysteeri enkä saanut sitä toimimaan, joten kokeilin komentoa ``git config core.editor notepad`` vaihtaakseni
editoriin, jota osaan käyttää. Sitten lisäsin commit-viestiksi edit user.name, add text to README.md. 

![image](https://github.com/RonjaVee/Palvelinten-hallinta/assets/148786247/5c5e414c-afaa-426b-9ce8-44a987c36164)

Sitten annoin komennot ``git pull`` (Already up to date) ja ``git push``. Tekemäni muokkaus näkyi nyt Githubissa. 

![image](https://github.com/RonjaVee/Palvelinten-hallinta/assets/148786247/e5201f37-725f-4d40-88b1-c5ae8ea67c7b)

c. Doh!

Tein uuden muutoksen README.md-tiedostoon "OHO! VIRHE. Kohta c.". Sitten annoin komennon ``git reset --hard``, ja muutokset hävisivät. (Pahoittelut rumista ääkkösistä kuvassa)

![image](https://github.com/RonjaVee/Palvelinten-hallinta/assets/148786247/d5a1c8f0-5d8e-40fd-9fcb-c2dccd20a0f2)

d. Tukki

Lokissa ``git log`` näkyy, että repositorioon on tehty yksi commit, tekijä on minä ja se on tehty 16.4. klo 17:49. Sitten lukee commit message. Alempana näkyy repositorion luoja ja luontiaika.

![image](https://github.com/RonjaVee/Palvelinten-hallinta/assets/148786247/3539121b-8f95-4a16-9e62-9e68f812becc)

e. Suolattu rakki

Loin salt-tialle oman kansion ``mkdir -p /srv/salt/``. Loin kansioon tiedoston esim.sls, ja sinne lisäsin

``/tmp/helloronja.txt:
   file.managed:
     - source: salt://helloronja.txt``

Sitten siirryin tekstitiedostoon ``notepad /srv/salt/helloronja.txt`` ja lisäsin sinne tekstin "Esimerkkiterveiset".

Palasin h3summer-repositorioon ja annoin komennon ``salt-call --local --file-root C:/srv/salt/ state.apply``.

![image](https://github.com/RonjaVee/Palvelinten-hallinta/assets/148786247/d90c456f-c13a-41bb-bdb9-db73215d30f9)

 Arvasinkin, että nyt on mennyt hommat vähän solmuun, joten lähdin takaisin srv/salt-kansioon ja poistin aiemman sls-tiedoston ja txt-tiedoston. Loin uuden hello.sls-tiedoston ja sinne laitoin 

``hello:
  cmd.run:
    - name: echo Hello, World! > C:\hello.txt``

![image](https://github.com/RonjaVee/Palvelinten-hallinta/assets/148786247/d11c63a1-8e0e-4305-a3d0-731dfe30787d)

Palasin h3summer-hakemistoon ja annoin komennon, ei toimi.

Katselin lisää ohjeita, ja tajusin, että ehkä srv/salt/-kansioon pitäisi tehdä vielä erillinen kansio, joten tein seuraavasti: 

![image](https://github.com/RonjaVee/Palvelinten-hallinta/assets/148786247/3e1632f6-8d2a-4e45-a4fe-4bcd878d15f7)

Eipä toimi, kaikkea samantapaista kokeilin. Pitääpä kerrata salt-tiloja ja niiden käyttöä, ja sitten vielä keksiä tähän tehtävään ratkaisu.  

Lopetus 18:50.

### Lähteet 

Tehtävä: Karvinen, Tero. Palvelinten hallinta 2024 kurssisivu. [https://terokarvinen.com/2024/configuration-management-2024-spring/](https://terokarvinen.com/2024/configuration-management-2024-spring/)

Chacon and Straub 2014: Pro Git, 2. painos, kohdasta 1.3 Getting Started - What is Git? [https://git-scm.com/book/en/v2/Getting-Started-What-is-Git%3F](https://git-scm.com/book/en/v2/Getting-Started-What-is-Git%3F)

Prajapati, Amit. What is git commit, push, pull, log, aliases, fetch, config & clone. Medium 20.9.2019. [https://medium.com/mindorks/what-is-git-commit-push-pull-log-aliases-fetch-config-clone-56bc52a3601c](https://medium.com/mindorks/what-is-git-commit-push-pull-log-aliases-fetch-config-clone-56bc52a3601c).

Karvinen, Tero. Hello Salt Infra-as-Code. 3.4.2024. [https://terokarvinen.com/2024/hello-salt-infra-as-code/](https://terokarvinen.com/2024/hello-salt-infra-as-code/)

OpenAI. "ChatGPT (GPT-3.5)". OpenAI API. 2024 [https://openai.com](https://openai.com) 



