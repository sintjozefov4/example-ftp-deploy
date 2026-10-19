# Je website online zetten met FTP

In dit voorbeeld wordt een website automatisch naar een webserver gekopieerd met GitHub Actions en FTP. Zo hoef je de bestanden niet na elke wijziging handmatig te uploaden.

## Wat heb je nodig?

- Een GitHub-account en een repository voor je project.
- Een website die lokaal werkt, bijvoorbeeld met een `index.html`-bestand.
- FTP-gegevens van je hostingprovider: de server, gebruikersnaam en het wachtwoord.
- Een FTP-account dat schrijfrechten heeft op de map waarin je website online moet komen.

## Eenmalig instellen

1. Zet de bestanden van je project in deze GitHub-repository. Zorg dat de startpagina (`index.html`) in de map staat die je wilt publiceren.
2. Open in GitHub je repository en ga naar **Settings > Secrets and variables > Actions**.
3. Voeg onder **Repository secrets** de volgende drie geheimen toe. Gebruik de namen precies zoals hieronder:

   | Naam | Waarde |
   | --- | --- |
   | `FTP_SERVER` | De FTP-server van je hostingprovider |
   | `FTP_USERNAME` | Je FTP-gebruikersnaam |
   | `FTP_PASSWORD` | Je FTP-wachtwoord |

   Bewaar je FTP-gegevens als secrets. Zet ze niet in je bestanden en deel ze niet in je code.
4. Controleer dat je repository een branch met de naam `main` heeft.

## Publiceren

De workflow in `.github/workflows/deploy.yml` start bij elke push naar `main`. GitHub Actions haalt dan de bestanden uit de repository op en synchroniseert ze met de FTP-server.

Je kunt publiceren door je wijzigingen naar `main` te pushen. Bekijk daarna het tabblad **Actions** in GitHub om te zien of de deployment is geslaagd. Na een geslaagde deployment kan het even duren voordat je wijzigingen zichtbaar zijn; vernieuw dan je website.

## Let op

- De FTP-server moet naar de juiste webmap schrijven. Controleer bij je hostingprovider welke map daarvoor bedoeld is en of je FTP-account daar toegang toe heeft.
- De workflow uploadt `.git`, `.github`, `.gitignore`, `README.md` en `AGENTS.md` niet. Deze uitsluitingen gelden ook voor gelijknamige mappen of bestanden in submappen.
- `.gitignore` bepaalt welke bestanden Git niet toevoegt aan je repository. Het is geen lijst met bestanden die de deployment automatisch overslaat.
- De deployment wordt alleen gestart bij een push naar `main`. Een wijziging in een andere branch wordt niet automatisch gepubliceerd.
