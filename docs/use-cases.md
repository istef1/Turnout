# Scenarii de utilizare

[← Înapoi la README](../README.md)

Scenariile urmează ecranele din [prototipul Figma](wireframes/README.md). Pentru fiecare scenariu sunt descrise:
- actorul și precondițiile;
- pașii;
- rezultatul așteptat;
- cazurile de eroare;
- cum se verifică.

Datele din exemple sunt cele din prototip.

---

## UC1. Înregistrare și autentificare

**Actor:** vizitator  
**Cerințe:** RF1, RF2, RF3, RF27  
**Ecrane:** [01 Autentificare](wireframes/01-autentificare.png) → [02 Înregistrare](wireframes/02-inregistrare.png) → [03 Evenimente](wireframes/03-evenimente.png)

**Pași:**
1. Maria deschide aplicația și ajunge pe ecranul „Autentificare”. Alege tabul „Înregistrare”.
2. Completează numele complet, adresa de e-mail și o parolă de cel puțin 8 caractere, apoi alege tipul de cont „Voluntar”.
3. Bifează „Sunt de acord cu prelucrarea datelor personale conform politicii de confidențialitate” și apasă „Creează contul”.

**Rezultat așteptat:**
- Contul este creat, iar acordul este salvat cu data acordării.
- Maria ajunge pe pagina „Evenimente”. În meniu vede „Evenimente”, „Campanii”, „Profil” și „Ieșire”, dar nu și „Panou coordonator”.

**Erori:**
- Fără bifa de acord, butonul „Creează contul” rămâne inactiv.
- Un e-mail deja folosit este respins cu `409` și mesajul „Există deja un cont cu acest e-mail”.
- O parolă mai scurtă de 8 caractere este respinsă și pe client, și pe server (`400`).
- Dacă cineva alege „Coordonator”, contul așteaptă aprobarea administratorului. Până atunci, autentificarea afișează „Contul de coordonator așteaptă aprobarea”.

**Verificare:** testul de API înregistrează un cont fără acord (`400`), apoi cu acord (`201`), apoi cu același e-mail (`409`).

---

## UC2. Căutarea unui eveniment și înscrierea

**Actor:** voluntar  
**Cerințe:** RF6, RF7, RF8, RF9, RF10, RF26  
**Ecrane:** [03 Evenimente](wireframes/03-evenimente.png) → [04 Detaliu eveniment](wireframes/04-detaliu-eveniment.png) → [05 Înscris](wireframes/05-detaliu-eveniment-inscris.png)

**Precondiții:** evenimentul „Plantare în Parcul Tineretului” (18 mai, 09:00–13:00, București, Sector 4) are 12 locuri libere.

**Pași:**
1. Maria alege locația „București” din filtru și scrie „plantare” în căutare.
2. Apasă „Detalii” pe cardul evenimentului.
3. Citește „Despre eveniment” și „Ce trebuie să aduci”, apoi apasă „Mă înscriu”.

**Rezultat așteptat:**
- După pasul 1, lista arată „1 evenimente găsite” și doar cardul căutat.
- După pasul 3:
  - apare eticheta „Ești înscris”;
  - mesajul se schimbă în „Locul tău este rezervat. Te așteptăm!”;
  - locurile libere scad la 11;
  - „Mă înscriu” se dezactivează, iar „Mă retrag” devine activ.
- Maria primește un e-mail de confirmare, iar coordonatorul vede o înscriere în plus.

**Erori:**
- Dacă nu mai sunt locuri, butonul „Mă înscriu” este dezactivat. Dacă cererea ajunge totuși la server, acesta răspunde cu `409` și mesajul „Nu mai sunt locuri libere”.
- O a doua înscriere la același eveniment este respinsă cu `409`.
- Dacă filtrele nu găsesc nimic, apare mesajul „Nu am găsit evenimente pentru filtrele selectate.”

**Verificare:** testul de API creează un eveniment cu un singur loc. Prima înscriere primește `201`, a doua `409`, iar după `DELETE` (retragere) locul redevine liber.

---

## UC3. Donația către o campanie

**Actor:** utilizator autentificat (donator)  
**Cerințe:** RF15, RF16, RF17, RF27  
**Ecrane:** [06 Campanii](wireframes/06-campanii-donatie.png) → [07 Donație confirmată](wireframes/07-donatie-confirmata.png)

**Precondiții:** campania „Ghiozdane pentru fiecare copil” a strâns 18.400 RON din 25.000 RON (74%), de la 126 de donatori, și mai are 18 zile.

**Pași:**
1. Maria deschide „Campanii” și selectează prima campanie. În formular apare „Pentru: Ghiozdane pentru fiecare copil”.
2. Alege suma de 100 RON.
3. Bifează acordul pentru prelucrarea datelor și apasă „Confirmă donația”.

**Rezultat așteptat:**
- Apare mesajul „Îți mulțumim! Donația ta de 100 RON a fost înregistrată în această simulare.”
- Campania arată 18.500 RON și 127 de donatori.
- Nu se cer și nu se salvează date de card.

**Erori:**
- Fără acord sau fără sumă, butonul „Confirmă donația” rămâne inactiv.
- O sumă mai mică de 1 RON este respinsă pe client (`min="1"`) și pe server (`400`).
- O donație către o campanie încheiată este refuzată cu mesajul „Campania s-a încheiat”.

**Verificare:** testul trimite o donație de 100 și verifică faptul că `GET /api/campaigns/:id` întoarce suma și numărul de donatori actualizate. Un al doilea test trimite `-5` și primește `400`.

---

## UC4. Panoul coordonatorului și exportul

**Actor:** coordonator  
**Cerințe:** RF3, RF11, RF12, RF18, RF22, RF23  
**Ecrane:** [08 Panou coordonator](wireframes/08-panou-coordonator.png)

**Pași:**
1. Andrei se autentifică cu un cont de coordonator aprobat și ajunge direct pe „Panou coordonator”.
2. Vede indicatorii (248 de voluntari activi, 14 evenimente în mai, 68.450 RON donații totale) și lista „Evenimente viitoare”.
3. Apasă „Eveniment nou”, completează formularul și salvează.
4. Apasă „Export CSV”.

**Rezultat așteptat:**
- Noul eveniment apare în „Evenimente viitoare” și în lista publică de evenimente.
- Apare notificarea „Fișierul CSV a fost pregătit.”, iar fișierul se descarcă.
- Exportul este salvat în jurnalul de audit.

**Erori:**
- Un eveniment cu ora de final înaintea orei de început sau cu număr de locuri ≤ 0 este respins (`400`), cu mesajul afișat lângă câmpul greșit.
- Un voluntar care cere `/api/reports/export.csv` primește `403`.

**Verificare:** testul cere exportul ca un coordonator (`200`, `Content-Type: text/csv`), apoi ca un voluntar (`403`).

---

## UC5. Gestionarea datelor personale (GDPR)

**Actor:** orice utilizator autentificat  
**Cerințe:** RF4, RF28, RF29, RF30  
**Ecrane:** [09 Datele mele](wireframes/09-datele-mele.png) → [10 Confirmare ștergere](wireframes/10-confirmare-stergere.png)

**Pași:**
1. Maria apasă „Profil” și ajunge pe „Datele mele”.
2. Își schimbă telefonul și apasă „Salvează modificările”.
3. Debifează „Comunicări despre oportunități”.
4. Apasă „Descarcă datele mele”.
5. Apasă „Șterge contul”, apoi „Da, șterge contul” în dialog.

**Rezultat așteptat:**
- După pasul 2, butonul afișează „Modificări salvate”.
- După pasul 3, Maria nu mai primește e-mailuri despre oportunități, iar retragerea acordului este salvată cu data ei.
- După pasul 4, se descarcă un fișier JSON cu profilul, participările, donațiile și acordurile.
- După pasul 5, Maria este deconectată și se întoarce la ecranul de autentificare. Datele ei personale se șterg în maximum 30 de zile, iar rapoartele păstrează doar totaluri anonime.
- Descărcarea și ștergerea apar în jurnalul de audit.

**Erori:**
- „Renunță” închide dialogul fără nicio modificare.
- Acordul „Prelucrarea datelor esențiale” nu se poate debifa, pentru că este necesar contului.

**Verificare:** după ștergere, `POST /api/auth/login` cu datele Mariei întoarce `401`, iar totalul donațiilor din raport rămâne același.
