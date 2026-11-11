# Scenarii de Utilizare 

Acest document descrie trei scenarii principale de utilizare (Use Cases) pentru aplicația **TurnOut**, detaliate pas cu pas și ușor de verificat.

---

## 1.  Înscrierea unui voluntar la o sarcină dintr-un eveniment

- **Actor principal:** Voluntar (autentificat)
- **Precondiții:** Utilizatorul este autentificat în aplicație și există un eveniment activ cu o sarcină care mai are locuri disponibile.
- **Postcondiții:** Voluntarul este înscris la sarcină, numărul de locuri disponibile scade cu 1, iar sistemul trimite un e-mail de confirmare.

### Fluxul principal:
1. Voluntarul accesează pagina de **Evenimente** și selectează un eveniment activ.
2. Aplicația afișează detaliile evenimentului și lista sarcinilor disponibile (cu locurile rămase).
3. Voluntarul apasă butonul **„Înscrie-te”** în dreptul sarcinii dorite.
4. Sistemul procesează cererea într-o tranzacție SQL, verifică dacă mai sunt locuri libere și creează înregistrarea.
5. Aplicația afișează un mesaj de succes și trimite automat un e-mail de confirmare prin SMTP.
6. Statusul sarcinii în interfață se actualizează (ex: „Înscris”).

### Fluxuri alternative / Excepții:
- **Locuri epuizate:** Dacă ultimul loc s-a ocupat înainte de procesare, sistemul afișează mesajul *„Nu mai sunt locuri disponibile pentru această sarcină”* și oprește înscrierea.
- **Înscriere duplicat:** Dacă voluntarul este deja înscris la sarcina respectivă, butonul este dezactivat / apare mesajul *„Ești deja înscris”*.

---

## 2. Crearea unui eveniment nou și definirea sarcinilor

- **Actor principal:** Coordonator
- **Precondiții:** Utilizatorul este autentificat cu rolul de Coordonator sau Admin.
- **Postcondiții:** Noul eveniment și sarcinile aferente sunt salvate în baza de date și devin vizibile public.

### Fluxul principal:
1. Coordonatorul accesează secțiunea **Dashboard Coordonator** și apasă pe **„Creează Eveniment Nou”**.
2. Completează formularul cu datele generale: titlu, descriere, dată/oră start și locație.
3. Adaugă una sau mai multe sarcini (ex: „Ghidaj vizitatori”, „Logistică”), specificând pentru fiecare titlul și numărul maxim de voluntari (locuri).
4. Apasă butonul **„Publică Eveniment”**.
5. Sistemul validează datele introduse și le salvează în PostgreSQL.
6. Aplicația redirecționează coordonatorul către pagina evenimentului nou creat.

### Fluxuri alternative / Excepții:
- **Date invalide:** Dacă un câmp obligatoriu lipsește sau data este în trecut, sistemul afișează erori de validare sub câmpurile aferente și previne trimiterea formularului.

---

## 3. Punctarea prezenței și validarea orelor de voluntariat

- **Actor principal:** Coordonator
- **Precondiții:** Evenimentul s-a încheiat sau este în desfășurare, iar voluntarii s-au înscris în prealabil.
- **Postcondiții:** Orele de voluntariat sunt disponibile în contul fiecărui voluntar prezent.

### Fluxul principal:
1. Coordonatorul deschide evenimentul din panoul de administrare și accesează secțiunea **„Management Prezență”**.
2. Aplicația afișează lista tuturor voluntarilor înscriși la sarcinile evenimentului.
3. Coordonatorul bifează voluntarii care au fost prezenți și introduce numărul de ore efectuate (sau confirmă numărul prestabilit).
4. Apasă pe **„Salvează și Validează Prezența”**.
5. Sistemul actualizează statusul fiecărei înscrieri (`Prezent`) și adaugă orele în profilul utilizatorilor corespunzători.
6. Aplicația afișează un mesaj de confirmare: *„Prezența a fost înregistrată cu succes”*.

### Fluxuri alternative / Excepții:
- **Absență voluntar:** Voluntarii nebifați sunt marcați ca `Absent`, iar numărul de ore adăugate pentru ei rămâne 0.
