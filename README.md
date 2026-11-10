# Turnout – platformă pentru coordonarea voluntarilor și a ONG-urilor

## 1. Descrierea proiectului

**Turnout** este o aplicație web destinată organizațiilor neguvernamentale (ONG-uri) mici și mijlocii, care își desfășoară activitatea în mare parte pe baza voluntarilor: asociații de cartier, organizații de mediu, bănci de alimente, asociații pentru copii sau vârstnici.

### Contextul

Un ONG care organizează, de exemplu, o campanie de curățenie, o colectare de alimente sau o strângere de fonduri pentru rechizite trebuie să țină evidența mai multor lucruri în același timp: cine sunt voluntarii și ce pot face, câți oameni sunt necesari la fiecare eveniment, ce materiale sunt disponibile, cât s-a donat și cum se raportează toate acestea finanțatorilor sau autorităților. În practică, aceste informații sunt împărțite între foi Excel, grupuri de mesagerie și e-mailuri, ceea ce face coordonarea dificilă și crește riscul de erori.

### Ce face aplicația

Turnout oferă un singur loc în care:

- **voluntarii** își creează un profil (competențe, disponibilitate), văd evenimentele programate, se înscriu sau se retrag și își urmăresc orele de voluntariat efectuate;
- **coordonatorii** creează evenimente și campanii, stabilesc numărul de voluntari necesari, confirmă prezența, înregistrează orele lucrate și alocă resursele (echipamente, materiale, săli);
- **donatorii** văd campaniile active, donează și urmăresc progresul față de obiectivul de fonduri;
- **administratorii ONG-ului** gestionează conturile și obțin rapoarte automate (ore de voluntariat, fonduri strânse, participare la evenimente), pe care le pot exporta.

### Protecția datelor

Aplicația prelucrează date personale (nume, e-mail, telefon, istoricul activității), așa că respectarea GDPR este parte din concept, nu o adăugire ulterioară. Utilizatorii își dau consimțământul la înregistrare, accesul la date este limitat în funcție de rol, se colectează doar datele necesare, iar fiecare persoană își poate descărca sau șterge datele din cont. Acțiunile asupra datelor personale sunt înregistrate într-un jurnal de audit.

## 2. Problema abordată

Multe ONG-uri își gestionează activitatea prin foi Excel, grupuri de WhatsApp și e-mailuri. Aceasta duce la:
- date împrăștiate și greu de actualizat (cine e voluntar activ, cine s-a înscris la ce eveniment);
- evenimente prost organizate (prea puțini sau prea mulți voluntari, lipsa resurselor);
- rapoarte realizate manual, consumatoare de timp;
- risc privind datele personale (liste cu telefoane și adrese e-mail distribuite necontrolat).

## 3. Obiective

1. Centralizarea datelor despre voluntari, campanii, donații, evenimente și resurse.
2. Simplificarea înscrierii voluntarilor la evenimente și a alocării lor pe sarcini.
3. Urmărirea transparentă a donațiilor și a progresului campaniilor.
4. Generarea automată de rapoarte (ore de voluntariat, fonduri strânse, participare).
5. Respectarea GDPR: consimțământ, acces pe roluri, dreptul la ștergerea datelor.

## 4. Utilizatori vizați

Aplicația se adresează atât persoanelor care participă la activitățile unui ONG, cât și celor care îl conduc. Am identificat patru roluri principale, fiecare cu nevoi diferite.

### 4.1. Voluntarul

**Cine este:** o persoană care dorește să se implice în activități comunitare, de la elevi și studenți până la angajați sau pensionari. Poate fi la prima experiență sau poate participa regulat.

**Nevoi:**
- să afle ușor ce evenimente există și când au loc;
- să se înscrie rapid, fără apeluri sau mesaje multiple;
- să știe exact ce are de făcut, unde și la ce oră;
- să aibă o dovadă a orelor de voluntariat (utilă, de exemplu, pentru CV sau pentru credite academice);
- să aibă control asupra datelor sale personale.

**În aplicație:** își creează profilul, caută și se înscrie la evenimente, primește confirmări și remindere, își vede istoricul și totalul orelor, își poate exporta sau șterge datele.

### 4.2. Coordonatorul de voluntari

**Cine este:** persoana din ONG responsabilă de organizarea activităților. Este adesea tot un voluntar sau un angajat cu normă redusă, care lucrează sub presiunea timpului.

**Nevoi:**
- să planifice evenimente fără să țină evidența pe foi separate;
- să vadă în timp real câți voluntari s-au înscris și dacă mai are nevoie de oameni;
- să aloce materialele și echipamentele necesare;
- să confirme prezența și să înregistreze orele efectuate;
- să creeze campanii și să vadă cum evoluează.

**În aplicație:** creează și editează evenimente și campanii, administrează înscrierile, alocă resurse, confirmă participarea.

### 4.3. Administratorul ONG-ului

**Cine este:** reprezentantul organizației (președinte, manager sau responsabil financiar), care răspunde de activitate în fața membrilor, a finanțatorilor și a autorităților.

**Nevoi:**
- să vadă o imagine de ansamblu asupra activității (voluntari activi, evenimente, fonduri strânse);
- să genereze rapoarte rapid, pentru finanțatori sau pentru rapoartele anuale;
- să controleze cine are acces la ce date;
- să se asigure că organizația respectă GDPR.

**În aplicație:** gestionează conturile și rolurile, consultă și exportă rapoarte, verifică donațiile .
### 4.4. Donatorul

**Cine este:** o persoană sau o firmă care vrea să sprijine financiar o cauză. Poate fi și voluntar, dar nu neapărat.

**Nevoi:**
- să înțeleagă clar pentru ce se strâng fondurile;
- să vadă cât s-a strâns față de obiectiv și că banii contează;
- să doneze simplu, fără formalități excesive;
- să știe ce se întâmplă cu datele sale.

**În aplicație:** vede campaniile active și progresul lor, face donații, își consultă istoricul donațiilor.


## 5. Funcționalități propuse

- Autentificare și gestionarea conturilor pe roluri
- Profil voluntar (competențe, disponibilitate)
- Creare și administrare evenimente, înscriere și confirmare participare
- Creare campanii cu obiectiv de fonduri și perioadă
- Înregistrarea și urmărirea donațiilor
- Gestionarea resurselor (materiale, echipamente, săli)
- Rapoarte și statistici (export CSV/PDF)
- Notificări prin e-mail
- Module GDPR: consimțământ, export și ștergere date personale

## 6. Tehnologii alese

| Componentă | Tehnologie |
|---|---|
| Frontend | React + Vite |
| Backend | Node.js + Express (API REST) |
| Bază de date | PostgreSQL |
| Autentificare | JWT + parole hash-uite (bcrypt) |
| Versionare | Git + GitHub |
| Documentație | Markdown, diagrame Mermaid |

Justificarea detaliată se află în [docs/implementation-plan.md](docs/implementation-plan.md).

## 7. Membrii echipei și responsabilități

Echipa este formată din două persoane. Responsabilitățile sunt împărțite astfel încât fiecare membru să contribuie atât la documentație, cât și la partea tehnică, iar deciziile importante (arhitectură, tehnologii, model de date) au fost discutate și luate împreună.

| Nume | Rol principal | Responsabilități | Documente asumate |
|---|---|---|---|
| **Irimia Denisa** | Backend, date și arhitectură | Proiectarea arhitecturii și a modelului de date, definirea endpoint-urilor API, autentificare și module GDPR, implementarea backend-ului | README.md, docs/architecture.md, docs/data-model.md, docs/implementation-plan.md |
| **Ivanik Ștefana** | Frontend, cerințe și interfață | Analiza cerințelor, scenariile de utilizare, proiectarea interfeței și a fluxurilor de navigare, implementarea frontend-ului | docs/requirements.md, docs/use-cases.md, docs/wireframes/ |

### Responsabilități comune

- stabilirea tehnologiilor și a strategiei de versionare;
- revizuirea reciprocă a documentelor și a Pull Request-urilor;
- testarea aplicației

## 8. Documentație

- [Cerințe funcționale și nefuncționale](docs/requirements.md)
- [Scenarii de utilizare](docs/use-cases.md)
- [Wireframe-uri și fluxuri de navigare](docs/wireframes/README.md)
- [Arhitectura aplicației](docs/architecture.md)
- [Modelul de date și endpoint-uri](docs/data-model.md)
- [Plan de implementare](docs/implementation-plan.md)
