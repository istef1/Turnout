# Cerințe

[← Înapoi la README](../README.md)

Prioritățile folosesc metoda MoSCoW:
- **M (Must):** obligatoriu pentru aplicația finală.
- **S (Should):** important, dar fără el aplicația tot funcționează.
- **C (Could):** opțional, se face doar dacă rămâne timp.

Coloana **P** arată prioritatea cerinței. Coloana **Ecran** arată în ce ecran din [prototipul Figma](wireframes/README.md) apare cerința. O liniuță (–) înseamnă că ecranul nu a fost încă desenat în prototip și va fi adăugat la Etapa 3.

## Roluri

| Rol | Cum se obține | Ce vede în prototip |
|---|---|---|
| **Voluntar** | Se alege „Voluntar” la înregistrare | Evenimente, Campanii, Profil |
| **Coordonator** | Se alege „Coordonator” la înregistrare. Contul devine activ după ce administratorul ONG îl aprobă. | Evenimente, Campanii, Panou coordonator, Profil |
| **Administrator ONG** | Contul este creat la instalarea aplicației și nu se poate obține prin înregistrare | Panou coordonator, plus pagini de administrare (nedesenate încă) |
| **Donator** | Nu este un tip de cont separat. Orice utilizator autentificat poate dona din pagina „Campanii”. | Campanii |

Toate paginile, cu excepția autentificării și a politicii de confidențialitate, cer un cont. După autentificare, voluntarul ajunge pe „Evenimente”, iar coordonatorul pe „Panou coordonator”.

## Cerințe funcționale

### Conturi și profil

| ID | Cerință | P | Ecran |
|---|---|---|---|
| RF1 | Un vizitator își creează cont cu nume complet, adresă de e-mail, parolă (minimum 8 caractere) și tip de cont (voluntar sau coordonator). Butonul „Creează contul” rămâne inactiv până când acceptă politica de confidențialitate. | M | 02 |
| RF2 | Utilizatorul se autentifică cu e-mail și parolă („Intră în cont”) și se poate deconecta („Ieșire”). | M | 01 |
| RF3 | Fiecare pagină și fiecare operație este permisă doar rolurilor potrivite. Meniul „Panou coordonator” apare doar pentru coordonatori. | M | 03, 08 |
| RF4 | În „Datele mele”, utilizatorul își modifică numele, e-mailul, telefonul și localitatea și apasă „Salvează modificările”. Primește confirmarea „Modificări salvate”. | M | 09 |
| RF5 | Voluntarul își poate trece în profil competențele și disponibilitatea. | S | – |

### Evenimente și înscrieri

| ID | Cerință | P | Ecran |
|---|---|---|---|
| RF6 | Lista de evenimente se poate căuta după titlu și filtra după dată (orice dată, săptămâna aceasta, luna aceasta) și locație (oraș). Ea arată numărul de rezultate („4 evenimente găsite”) și este sortată după data cea mai apropiată. | M | 03 |
| RF7 | Fiecare card de eveniment arată categoria, titlul, data, locația, locurile libere și butonul „Detalii”. Dacă niciun eveniment nu se potrivește, apare mesajul „Nu am găsit evenimente pentru filtrele selectate.” | M | 03 |
| RF8 | Pagina evenimentului arată categoria, titlul, data și ora, locația, numărul de locuri libere, descrierea („Despre eveniment”) și ce trebuie adus („Ce trebuie să aduci”). | M | 04 |
| RF9 | Voluntarul apasă „Mă înscriu” și primește confirmarea prin e-mail. Pe pagină apare eticheta „Ești înscris” și mesajul „Locul tău este rezervat. Te așteptăm!”. Butonul „Mă înscriu” se dezactivează, iar butonul „Mă retrag” devine activ. | M | 04, 05 |
| RF10 | Înscrierea este posibilă doar dacă mai sunt locuri libere. Voluntarul se poate retrage cu „Mă retrag”, iar locul se eliberează. | M | 04, 05 |
| RF11 | Coordonatorul creează un eveniment nou din butonul „Eveniment nou” și poate modifica sau șterge evenimentele lui. Câmpurile unui eveniment sunt titlu, categorie, dată, interval orar, locație, număr de locuri, descriere și ce trebuie adus. | M | 08 |
| RF12 | Coordonatorul vede evenimentele viitoare (data, titlul, locația, intervalul orar și locurile libere) și le deschide din panou. | M | 08 |
| RF13 | Coordonatorul vede lista voluntarilor înscriși la un eveniment, îi repartizează pe sarcini și confirmă prezența. Orele se calculează automat. | M | – (meniul „Voluntari” din 08) |
| RF14 | Voluntarul își vede istoricul participărilor și totalul de ore. | M | – |

### Campanii și donații

| ID | Cerință | P | Ecran |
|---|---|---|---|
| RF15 | Pagina „Campanii” arată campaniile active. Pentru fiecare se văd titlul, suma strânsă (RON), procentul, bara de progres, obiectivul, numărul de donatori și zilele rămase. | M | 06 |
| RF16 | Utilizatorul alege o campanie, introduce suma în RON (sau alege 50, 100 sau 200 RON), bifează acordul pentru prelucrarea datelor și apasă „Confirmă donația”. Butonul rămâne inactiv fără acord sau fără sumă. | M | 06 |
| RF17 | Plata este simulată, iar formularul afișează mesajul „Plată simulată. Nu se procesează bani reali.” După confirmare apare mesajul „Îți mulțumim!” și butonul „Donează din nou”. Suma strânsă și numărul de donatori se actualizează. | M | 07 |
| RF18 | Coordonatorul creează campanii („Campanie nouă”), cu titlu, descriere, obiectiv (RON) și dată de final, și le poate modifica sau închide. | M | 08 |
| RF19 | Utilizatorul își vede istoricul donațiilor. | S | – |

### Resurse

| ID | Cerință | P | Ecran |
|---|---|---|---|
| RF20 | Coordonatorul gestionează inventarul de resurse: echipamente, materiale și săli. | M | – (meniul „Resurse” din 08) |
| RF21 | Coordonatorul alocă resurse unui eveniment. Nu se pot aloca mai multe bucăți decât sunt disponibile și nici aceeași sală la două evenimente care se suprapun. | M | – |

### Panou, rapoarte și export

| ID | Cerință | P | Ecran |
|---|---|---|---|
| RF22 | Panoul coordonatorului arată voluntarii activi, evenimentele din luna curentă și donațiile totale, fiecare cu o comparație scurtă (de exemplu „+12 luna aceasta”). | M | 08 |
| RF23 | Butonul „Export CSV” descarcă datele panoului (voluntari, participări, donații). „Raport lunar” generează raportul pe luna curentă. | M | 08 |
| RF24 | Raportul se poate exporta și în PDF. | C | – |
| RF25 | Coordonatorul importă voluntari sau resurse dintr-un fișier CSV. Rândurile invalide apar într-un raport de erori. | M | – |
| RF26 | Utilizatorul primește un e-mail de confirmare la înscriere, un reminder cu 24 de ore înainte de eveniment și o notificare dacă evenimentul se modifică. | S | 04 (mesajul despre e-mail) |

### Administrare și GDPR

| ID | Cerință | P | Ecran |
|---|---|---|---|
| RF27 | La înregistrare, utilizatorul acceptă prelucrarea datelor. Acordul pentru donație se cere separat, în formularul de donație. | M | 02, 06 |
| RF28 | În „Acorduri și comunicări”, utilizatorul vede acordul obligatoriu („Prelucrarea datelor esențiale”) și poate activa sau retrage acordurile opționale: „Comunicări despre oportunități” și „Analiză și îmbunătățirea platformei”. | M | 09 |
| RF29 | Butonul „Descarcă datele mele” oferă o copie a datelor personale într-un format ușor de citit (JSON). | M | 09 |
| RF30 | Butonul „Șterge contul” deschide dialogul „Confirmi ștergerea contului?”, cu butoanele „Renunță” și „Da, șterge contul”. După confirmare, utilizatorul este deconectat. Datele personale și istoricul participărilor se șterg sau se anonimizează în maximum 30 de zile, iar în rapoarte rămân doar totaluri anonime. | M | 10 |
| RF31 | Administratorul ONG aprobă conturile de coordonator, dezactivează conturi și vede jurnalul de audit (accesări de date personale, exporturi, ștergeri). | M | – |

## Cerințe nefuncționale

| ID | Categorie | Cerință | P |
|---|---|---|---|
| RNF1 | Securitate | Parolele se salvează doar ca hash (bcrypt). Token-urile JWT expiră după un timp limitat. Secretele stau în `.env`, nu în repository. | M |
| RNF2 | Securitate | Toate datele primite sunt validate pe server, iar rolul este verificat la fiecare cerere către API. Un cont de coordonator neaprobat nu are acces la operațiile de coordonator. | M |
| RNF3 | Securitate | Interogările SQL sunt parametrizate. React escapează automat textul afișat, iar `dangerouslySetInnerHTML` nu este folosit. | M |
| RNF4 | Confidențialitate | Fiecare rol vede doar datele de care are nevoie. Datele de contact ale voluntarilor sunt vizibile doar coordonatorilor. | M |
| RNF5 | Accesibilitate | Toate câmpurile au etichetă (inclusiv căutarea și filtrele, prin etichete ascunse vizual). Butoanele au minimum 44 px înălțime, iar butonul de meniu are text alternativ („Deschide meniul”). Dialogul de ștergere este marcat `role="dialog"`. Contrastul textului este de cel puțin 4.5:1. | M |
| RNF6 | Responsive | Interfața funcționează de la 320 px până la desktop. Pe telefon, meniul devine hamburger, coloanele trec una sub alta, iar butoanele principale ocupă toată lățimea. | M |
| RNF7 | Utilizabilitate | Fiecare acțiune are confirmare vizibilă: mesaje de tip „Modificări salvate”, notificări temporare în panou și butoane dezactivate când acțiunea nu este posibilă. | M |
| RNF8 | Consecvență vizuală | Interfața folosește stilul din prototip: alb, negru și gri, fără colțuri rotunjite, cu etichete mici scrise cu majuscule (de exemplu „OPORTUNITĂȚI DE VOLUNTARIAT”). | S |
| RNF9 | Mentenabilitate | Componentele reutilizate din prototip (`Button`, `Field`, `Checkbox`, `PageHeader`, `TopBar`, `Icon`) devin componente React separate. README-ul conține pașii de instalare și rulare. | M |
| RNF10 | Testare | Fluxurile principale și cazurile de eroare sunt acoperite de teste automate pentru API. | M |

## Ce nu intră în proiect

- Procesarea plăților reale. Donațiile sunt simulate.
- SMS-uri și o aplicație mobilă nativă.
- Contabilitatea și facturarea ONG-ului.
- Mai multe ONG-uri în aceeași instanță. Fiecare ONG își rulează propria instanță a aplicației.
