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
<img width="1442" height="193" alt="imagen" src="https://github.com/user-attachments/assets/9b848f75-8371-406b-99de-9fd62d9bda19" />
<img width="1442" height="193" alt="imagen" src="https://github.com/user-attachments/assets/4c55b7a6-e4c5-4ddb-817b-4f34e0d37720" />
<img width="1421" height="169" alt="imagen" src="https://github.com/user-attachments/assets/bba7d487-5b5f-42af-b9b3-e625e08f0645" />
<img width="1238" height="203" alt="imagen" src="https://github.com/user-attachments/assets/caed4061-2a74-4443-90a1-34370a9a9f80" />

## Evidències de Funcionament

*(Aquí s'haurien d'adjuntar les captures de pantalla segons la pràctica)*
