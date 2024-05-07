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
