# Planul de implementare
## 1. Justificarea tehnologiilor alese

Aplicația folosește o arhitectură web 3-tier (Frontend, Backend, Bază de date), aleasă pentru performanță, modularitate și securitate:

- **React + Vite (Frontend):** Permite construirea unei interfețe rapide, bazată pe componente reutilizabile (formulare, tabele, carduri) 
- **Node.js + Express (Backend):** Oferă un mediu asincron ideal pentru tratarea cererilor HTTP REST API, gestionarea middleware-urilor de securitate (JWT) și trimiterea notificărilor prin e-mail .
- **PostgreSQL (Bază de date):** Garantează integritatea datelor prin constrângeri SQL (FOREIGN KEY, CHECK) și previne supra-înscrierea la sarcini prin gestionarea securizată a tranzacțiilor și blocarea la nivel de rând (FOR UPDATE).
---

## 2. Strategia de versionare și fluxul de lucru Git

Gestionarea codului se face pe **GitHub** folosind un flux simplificat de lucru (**GitHub Flow**):

- **`main`:** Ramura principală care stochează doar codul stabil și documentația finală.
- **`feature/*`:** Ramuri dedicate pentru dezvoltarea fiecărei funcționalități sau fișier (ex: `feature/auth`, `feature/events-api`).
- **Pull Requests (PR):** Codul este îmbinat în `main` doar prin PR-uri verificate de colega de echipă.
- **Prefixe Commit:** `feat:` (funcționalitate nouă), `docs:` (documentație), `fix:` (remediere erori).

---

## 3. Planul de implementare și prioritizarea activităților

Dezvoltarea este structurată în 4 etape principale:

- **Etapa 1: Documentație & Design** – Cerințe, arhitectură, model de date și wireframes.
- **Etapa 2: Arhitectură de Bază & Autentificare** – Setup PostgreSQL, server Express, autentificare JWT și roluri.
- **Etapa 3: Module Principale** – Implementare API & UI pentru evenimente, înscrieri, campanii de donații și resurse.
- **Etapa 4: Finisare & Securitate** – Testare, integrări SMTP, optimizări și securizare.

### Prioritizarea funcționalităților (Metoda MoSCoW)
- **Must Have:** Autentificare/Autorizare (JWT), CRUD Evenimente & Sarcini, Înscriere voluntari cu limită de locuri (tranzacțional), Vizualizare campanii.
- **Should Have:** Notificări e-mail (SMTP), Istoric activitate în contul propriu, Punctare prezență voluntari.
- **Could Have:** Modul inventar resurse, Generare adeverință voluntariat (PDF).
- **Won't Have:** Plăți online direct prin card (Stripe live), încărcare fișiere/imagini pe server.

---

## 4. Repartizarea responsabilităților la implementare

Responsabilitățile tehnice sunt împărțite pe cele două mari componente ale aplicației (Backend și Frontend), deciziile privind arhitectura și integrările fiind luate de comun acord:

| Membru Echipă | Rol în implementare | Module și componente tehnice asumate |
|---|---|---|
| **Irimia Denisa** | Backend & Database Developer | - Crearea schemei bazei de date PostgreSQL (`schema.sql`, `seed.sql`) și tranzacțiile SQL pentru înscrieri.<br/>- Structurarea serverului Node.js cu Express (controllere, servicii, rute API REST).<br/>- Implementarea securității: middleware-uri de autentificare (JWT) și autorizare pe roluri.<br/>- Trimiterea de notificări prin e-mail (`Nodemailer` + SMTP).<br/>- Funcționalitatea GDPR de anonimizare/ștergere date. |
| **Ivanik Ștefana** | Frontend Developer | - Configurarea aplicației  cu React + Vite și definirea rutelor (`react-router`).<br/>- Implementarea componentelor UI refolosibile (formulare cu validare, tabele cu paginare, carduri).<br/>- Crearea paginilor publice (Acasă, Liste Evenimente și Campanii, Autentificare).<br/>- Crearea ecranelor protejate (Contul meu pentru voluntari/donatori, dashboard-ul coordonatorului și al adminului).<br/>- Clientul API (modulul centralizat cu `fetch` pentru transmiterea token-ului JWT și tratarea erorilor HTTP). |
