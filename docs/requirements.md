# Analiza Cerințelor (Requirements)

Acest document prezintă cerințele funcționale și nefuncționale ale aplicației **TurnOut**, precum și prioritizarea acestora.

---

## 1. Cerințe Funcționale

-  Utilizatorii se pot înregistra și autentifica securizat (cu e-mail și parolă), primind acces în funcție de rol (Voluntar, Donator, Coordonator, Admin).
-  Coordonatorii pot crea evenimente cu sarcini și locuri limitate, iar voluntarii se pot înscrie sau anula înscrierea la aceste sarcini.
-  Coordonatorii pot bifa prezența voluntarilor la finalul evenimentului și pot valida orele de voluntariat efectuate.
-  Vizualizarea campaniilor de strângere de fonduri și înregistrarea donațiilor financiare.
-  Trimiterea de e-mailuri de confirmare prin server SMTP la înscrierea la un eveniment.

---

## 2. Cerințe Nefuncționale

-  Parolele sunt criptate cu `bcrypt`, iar rutele private din API sunt protejate prin token-uri JWT.
-  Gestionarea sigură a locurilor limitate la sarcini pentru a preveni supra-înscrierea voluntarilor.
-  Interfață web responsive, adaptată pentru browsere moderne, desktop și mobil.
-  Interfață web responsive și intuitivă, optimizată pentru browsere moderne, tablete și telefoane mobile.

---

## 3. Prioritizarea Cerințelor (Metoda MoSCoW)

| Categorie | Descriere |
|---|---|
| **Must Have** *(Obligatoriu)* | Autentificare și roluri (JWT), vizualizare și creare evenimente, înscriere voluntari cu limită de locuri. |
| **Should Have** *(Important)* | Punctare prezență voluntari, modul campanii și donații, trimitere e-mailuri de confirmare (SMTP). |
| **Could Have** *(Opțional)* | Generare adeverință de voluntariat (PDF), opțiuni de anonimizare cont (GDPR). |
| **Won't Have** *(Nu se include)* | Procesare plăți online cu cardul în timp real, încărcare de fișiere/imagini pe server. |
