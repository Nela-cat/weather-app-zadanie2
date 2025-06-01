WeatherApp - Zadanie 2

Aneliia Henina

1. Budowa obrazu:
   docker build -t test_ci_app .
   
2. Uruchomienie kontenera:
   docker run -p 8000:8000 test_ci_app
   
3. Konfiguracja sekretów GitHub
   1. GHCR_PAT - Personal Access Token (PAT)
   2. DOCKERHUB_USERNAME - Login do konta DockerHub
   3. DOCKERHUB_TOKEN - Token wygenerowany na stronie DockerHub
