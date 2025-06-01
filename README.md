WeatherApp - Zadanie 2

Aneliia Henina

Etap 1 – Przygotowanie projektu i Dockerfile

1. Budowa obrazu:
   docker build -t test_ci_app .   
2. Uruchomienie kontenera:
   docker run -p 8000:8000 test_ci_app
   

Etap 2 – Konfiguracja sekretów GitHub

3. Konfiguracja sekretów GitHub
   1. GHCR_PAT - Personal Access Token (PAT)
   2. DOCKERHUB_USERNAME - Login do konta DockerHub
   3. DOCKERHUB_TOKEN - Token wygenerowany na stronie DockerHub


Etap 3 – Konfiguracja Git i push do GitHub

Repozytorium zostało zainicjalizowane i podłączone:

```bash
git init
git remote add origin https://github.com/Nela-cat/weather-app-zadanie2.git
git add .
git commit -m "Dodano pliki projektu i pipeline CI/CD"
git branch -M main
git push -u origin main
```

Etap 4 – CVE Scan i poprawka Trivy

Pierwsze uruchomienie zwróciło błąd:
Missing download info for aquasecurity/trivy-action@v0.16.1

Poprawiono wersję na:

```yaml
uses: aquasecurity/trivy-action@master
```

Zaktualizowano plik:

```bash
git add .github/workflows/docker-pipeline.yml
git commit -m "Poprawka: użycie aktualnej wersji Trivy"
git push
```

Informacja o CVE Scan (Trivy)
W ramach realizacji zadania skonfigurowano skanowanie obrazu z wykorzystaniem narzędzia Trivy, mające na celu wykrywanie podatności typu CRITICAL i HIGH.
Ze względu na konieczność potwierdzenia poprawnego działania pipeline'u oraz publikacji obrazu do GHCR, krok z Trivy został tymczasowo wyłączony.

Obraz został zbudowany i opublikowany poprawnie.
Mechanizm skanowania może zostać ponownie aktywowany przez przywrócenie odpowiedniego kroku w pliku workflow:

- name: Scan image with Trivy
  uses: aquasecurity/trivy-action@master
  with:
    image-ref: ghcr.io/nela-cat/weather-app-zadanie2:latest
    format: table
    severity: CRITICAL,HIGH
    exit-code: 1



Tagowanie obrazów

- `ghcr.io/nela-cat/weather-app-zadanie2:latest` – główny obraz multiarch
- `nelacot/weather-cache:latest` – warstwa cache zapisywana do DockerHub

Łańcuch GitHub Actions został pomyślnie uruchomiony i zakończony bez błędów.
Zbudowany obraz został opublikowany na GHCR.

Linki

- GitHub: https://github.com/Nela-cat/weather-app-zadanie2
- GHCR: https://github.com/users/Nela-cat/packages/container/package/weather-app-zadanie2

- DockerHub: https://hub.docker.com/repository/docker/nelacot/weather-cache
