# Pràctica: Proxies amb Nginx

Aquest projecte implementa una infraestructura de serveis web amb Docker Compose que inclou dos nodes Apache darrere d'un proxy invers Nginx amb balanceig de càrrega i memòria cau.

## Estructura del Projecte

- `docker-compose.yml`: Configuració dels contenidors Apache i Nginx.
- `nginx/nginx.conf`: Configuració detallada de Nginx (proxy, load balancing, cache).
- `web/`: Directori amb el contingut web compartit.
  - `index.html`: Pàgina principal.
  - `imatge.jpg`: Imatge de prova.
  - `video.mp4`: Vídeo de prova.

## Fases realitzades

1.  **Nodes Web**: S'han configurat dos contenidors Apache que serveixen el mateix contingut.
2.  **Volum Compartit**: Ambdós nodes utilitzen el directori local `./web` muntat com a volum.
3.  **Proxy Invers i Balanceig**: Nginx actua com a punt d'entrada i distribueix el trànsit entre `apache1` i `apache2` utilitzant Round Robin.
4.  **Memòria Cau**: Nginx emmagatzema en memòria cau les respostes dels backends per millorar el rendiment.

## Com provar el funcionament

1.  Aixecar la infraestructura:
    ```bash
    docker compose up -d
    ```

2.  Verificar el balanceig de càrrega:
    - Accediu a `http://localhost`.
    - Podeu revisar els logs de docker per veure quins nodes responen: `docker compose logs -f`.

3.  Verificar la memòria cau (HIT/MISS):
    - Utilitzeu `curl` per veure les capçaleres:
      ```bash
      curl -I http://localhost
      ```
    - Busqueu la capçalera `X-Cache-Status`. La primera petició hauria de ser `MISS` i les següents `HIT`.



## Evidències de Funcionament
Contenedor funcionando.
<img width="1458" height="155" alt="imagen" src="https://github.com/user-attachments/assets/dfc2ee4e-f549-4ec3-ad5e-e8b2bed95396" />

Web local funcionando.
<img width="1917" height="962" alt="imagen" src="https://github.com/user-attachments/assets/db2263b2-92a2-4576-bc0d-5b057f888033" />

Round Robin funcionando.
<img width="1257" height="567" alt="imagen" src="https://github.com/user-attachments/assets/32457554-62ea-4cde-be2e-3c4eab7d651c" />

Peticions cache Miss i Hit.
<img width="1617" height="202" alt="imagen" src="https://github.com/user-attachments/assets/0617583c-6758-4d76-b85a-0bce52591830" />
<img width="1238" height="203" alt="imagen" src="https://github.com/user-attachments/assets/caed4061-2a74-4443-90a1-34370a9a9f80" />
<img width="1442" height="193" alt="imagen" src="https://github.com/user-attachments/assets/4c55b7a6-e4c5-4ddb-817b-4f34e0d37720" />
<img width="1421" height="169" alt="imagen" src="https://github.com/user-attachments/assets/bba7d487-5b5f-42af-b9b3-e625e08f0645" />

