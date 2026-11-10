# Modelul de date și API-ul aplicației


Acest document prezintă modelul preliminar de date (entitățile și relațiile din PostgreSQL) și principalele servicii/endpoint-uri API REST ale aplicației Turnout.

---

## 1. Entități și Relații

- **`USERS`**: Stochează utilizatorii aplicației (voluntari, donatori, coordonatori, admini).
  - *Relații:* Are mai multe `REGISTRATIONS` (ca voluntar) și mai multe `DONATIONS` (ca donator).
- **`EVENTS`**: Evenimentele organizate de ONG.
  - *Relații:* Conține una sau mai multe `TASKS`.
- **`TASKS`**: Sarcinile specifice din cadrul unui eveniment.
  - *Relații:* Aparține unui `EVENT`; are înscrise mai multe `REGISTRATIONS` și folosește mai multe `TASK_RESOURCES`.
- **`REGISTRATIONS`**: Înscrierile voluntarilor pe sarcini specifice.
  - *Relații:* Face legătura între `USERS` și `TASKS` (gestionează locurile și statusul prezenței).
- **`CAMPAIGNS`**: Campaniile de strângere de fonduri.
  - *Relații:* Primește mai multe `DONATIONS`.
- **`DONATIONS`**: Tranzacțiile/donațiile financiare efectuate.
  - *Relații:* Face legătura între `USERS` și `CAMPAIGNS`.
- **`RESOURCES`**: Inventarul fizic de echipamente al ONG-ului.
  - *Relații:* Alocat pe sarcini prin `TASK_RESOURCES`.

---

## 2. Servicii și Endpoint-uri Principale

Toate rutele folosesc formatul **JSON** și sunt prefixate cu `/api`. Rutele protejate necesită un token **JWT** valid.

### Autentificare & Utilizatori
- `POST /api/auth/login` – Autentificare utilizator și generare token JWT.
- `POST /api/auth/register` – Înregistrare voluntar sau donator nou.
- `GET /api/users/me` – Vizualizare profil propriu și ore de voluntariat.

### Evenimente & Înscrieri
- `GET /api/events` – Listare evenimente active (Public).
- `POST /api/events` – Creare eveniment nou (Coordonator / Admin).
- `POST /api/events/:id/registrations` – Înscriere voluntar la o sarcină.
- `PATCH /api/registrations/:id/attendance` – Marcare prezență și validare ore (Coordonator).

### Donații & Campanii
- `GET /api/campaigns` – Listare campanii de strângere de fonduri (Public).
- `POST /api/campaigns/:id/donations` – Înregistrare donație pentru o campanie.

### Resurse (Inventar)
- `GET /api/resources` – Consultare inventar echipamente (Coordonator / Admin).
- `POST /api/tasks/:id/resources` – Alocare resurse pentru o sarcină (Coordonator).
