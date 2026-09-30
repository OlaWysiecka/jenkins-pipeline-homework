# Jenkins Pipeline Homework

## Opis

Projekt przedstawia zaawansowany pipeline Jenkins z obsługą błędów,
warunkowym wykonywaniem etapów, zmiennymi środowiskowymi oraz
raportowaniem wyniku pipeline'u.

## Etapy pipeline'u

Pipeline składa się z czterech etapów:

1. Checkout - pobranie kodu z repozytorium.
2. Build - budowanie aplikacji.
3. Test - uruchomienie testów.
4. Deploy - symulacja wdrożenia.

## Obsługa błędów

Każdy etap wykorzystuje blok `try-catch`.

W przypadku błędu wykonywana jest instrukcja `error()`, która oznacza
pipeline jako nieudany.

## Zmienne środowiskowe

Pipeline wykorzystuje:

- `APP_VERSION` - wersja aplikacji.
- `DEPLOY_ENVIRONMENT` - środowisko wdrożenia.
- `APP_NAME` - nazwa aplikacji.

## Warunki

Etapy Build, Test i Deploy są wykonywane warunkowo.

Deploy zostanie wykonany tylko wtedy, gdy:

- wcześniejsze etapy zakończyły się sukcesem,
- `DEPLOY_ENVIRONMENT` ma wartość `production`.

## Post actions

Pipeline posiada:

- `success` - komunikat po sukcesie,
- `failure` - komunikat po błędzie,
- `always` - komunikat wykonywany zawsze.

## Uruchamianie lokalne

Instalacja zależności:

```bash
python -m pip install -r requirements.txt
```
Uruchomienie aplikacji:
```bash
python app.py
```

Uruchomienie testów:
```bash
python -m pytest -v
```

## Jenkins
Jenkins powinien korzystać z pliku Jenkinsfile znajdującego się
w repozytorium GitHub.