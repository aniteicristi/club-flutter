# Introducere in Git

Ce este un proiect?

Putem sa vedem un proiect ca un set de documente intr-un folder. In felul acesta suntem obisnuiti sa lucram cu un proiect, mai ales in cele din C++, sau in alte limbaje. Acest sistem este foarte simplu, mai ales cand suntem singura persoana care lucreaza pe acel fisier. Problema apare in momentul in care sunt mai mult decat 2 persoane...

Sa spunem ca **A**na, **B**ogdan si **C**atalina au fost adaugate pe acelasi proiect. Intrebarea este, cum pot aceste 3 persoane, care lucreaza in paralel sa contribuie in mod constructiv unui singur proiect? Ei bine, GIT vine ca raspuns la exact aceasta problema.

# O explicatie intuitiva

Ok, sa spunem ca Ana, Bogdan si Catalina sunt scenariste la Marvel (adica se ocupa cu scrierea scenariului pentru filmele marvel)

Intr-o zi, directorul creativ Marvel, Kevin Feige, vine la ei si spune:

> "Ok baieti, deci trebuie sa scriem un nou film despre Capitanul America. Initial filmul incepe cu capitanul america care sta la o cafea pe strada Eroilor in Cluj. Ce facem de acolo?"

Incantati de ideea de a refolosi un personaj drag care canonic e pensionat din univers, fiecare scenarist se pune si isi scrie propria versiune de scenariu.

Ana zice:

- Cap America sta la cafea
- Thanos vine cu o nava spatiala
- Clujul e in pericol.
- Cap America se infiltreaza prin usa din spate
- Cap America se duce si ii da un pumn la Thanos.

Bogdan zice:

- Cap America sta la cafea
- Thanos apare de sub pamant cu un burghiu urias
- Cetatenii din cluj sunt speriati.
- Cap America se duce si il loveste pe Thanos cu scutul lui.

Bogdan iși termina povestea mult mai repede, deoarece are mai putine scene, asa ca el o inainteaza manager-ului sau **Git**ță primul, deci povestea sa se comporta ca o baza.

Ana, ulterior, isi termina si ea povestea si doreste sa o inainteze managerului. Dar, acum, povestea este scrisa de catre Bogdan, asa ca Gitță ii zice anei:

> "Uite, ce ai scris tu nu se potriveste cu ce a scris Bogdan. Bogdan a terminat mai repede, deci este responsabilitatea ta sa iti introduci modificarile si povestea sa aiba sens."

Ana, se uita la cele doua povesti. Prima scena, este la fel, deoarece amandoi au inceput de la aceasi baza.

Observa ca la scena a doua, Thanos vine cu o nava spatiala in versiunea Anei, in timp ce in versiunea lui Bogdan vine cu un burghiu urias. Anei i se pare o prostie ce a scris Bogdan, asa ca alege sa pastreze ce a scris ea si sa dea delete la ce a scris bogdan.

```
- Cap America sta la cafea
- Thanos vine cu o nava spatiala
```

Ana observa, atat ea cat si Bogdan au spus doua lucruri care nu se contrazic, si anume ca Clujul e in pericol, si cetatenii sunt speriati. Asa ca alege sa le pastreze pe amandoua:

```
- Cap America sta la cafea
- Thanos vine cu o nava spatiala
- Cetatenii din cluj sunt speriati.
- Clujul e in pericol.
```

Ana observa ca Bogdan nu a specificat cum intra Cap America in nava lui thanos, asa ca poate sa isi pastreze scena cu infiltrarea.

```
- Cap America sta la cafea
- Thanos vine cu o nava spatiala
- Cetatenii din cluj sunt speriati.
- Clujul e in pericol.
- Cap America se infiltreaza prin usa din spate
```

La final, mai apare un conflict, si anume felul in care e infrant Thanos. Anei i se pare ca varianta lui Bogdan e mai buna, asa ca o pastreaza pe a lui, iar povestea ajunge sa fie:


```
- Cap America sta la cafea
- Thanos vine cu o nava spatiala
- Cetatenii din cluj sunt speriati.
- Clujul e in pericol.
- Cap America se infiltreaza prin usa din spate
- Cap America se duce si il loveste pe Thanos cu scutul lui.
```

Multumita de modificarile facute, Ana isi inainteaza schimbarile ei combinate cu schimbarile lui Bogdan la manager, iar aceasta poveste devine noua poveste oficiala.

Catalina vine din pauza de pranz si doreste sa scrie si ea, asa ca se duce la manager si il intreaba cum e scenariul. Gitță ii da ultima versiune a scenariului. Catalina vazand ca au fost facute deja modificari, nu doreste sa le strice munca celor doi, asa ca continua sa scrie in continuare.

```
- Cap America sta la cafea
- Thanos vine cu o nava spatiala
- Cetatenii din cluj sunt speriati.
- Clujul e in pericol.
- Cap America se infiltreaza prin usa din spate
- Cap America se duce si il loveste pe Thanos cu scutul lui.
- Nava explodeaza
- Cap America nu este gasit dupa explozie
- La final, este o scena cu cap America cum continua sa isi bea cafeaua, in secret
```

Cand e gata isi trimite ultima versiune la Gitță. Managerul se uita si vede ca modificarile ei sunt compatibile si au sens fata de ultima versiune, asa ca le accepta.

Desigur, scenaristii nu lucreaza asa, dar programatorii  lucreaza in felul acesta

In aceasta metafora, Gitță este `Git`, managerul care se asigura ca modificarile aduse scenariului au sens si nu exista conflicte intre ce scrie Ana, Bogdan si Catalina.

La inceput, fiecare scenarist si-a facut o copie a scenariului, care continea doar prima scena. Aceste copii se numesc `branch`-uri.

Fiecare persoana isi aduce modificarile in branch-ul lui. Aceste modificari se numesc `commit`-uri.

La final, atat Ana cât și Bogdan vor sa își înnainteze modificarile la scenariul initial. Aceasta operațiune se numește `merge`.

Deoarece Bogdan a fost primul care a dat `merge`, el nu a avut conflicte, deoarece doar a adaugat la ce era inainte.

Ana, ulterior, a vrut si ea să dea `merge`, dar modificarile ei au intrat in conflict cu versiunea "oficiala" a lui Bogdan. Asa ca ana a trebuit sa faca una din 3 operatii pentru fiecare linie care nu se potrivea:

- `Keep Both` (situatia clujului)
- `Accept theirs` (felul in care thanos este invins)
- `Accept mine` (cum ajunge thanos in cluj)

La final, Catalina vine la git și ii cere versiunea oficiala. Asta inseamna ca Catalina a facut operația de `pull`.

O data ce Cătălina are versiunea oficiala, și ea își creaza un `branch` pe care sa lucreze, si la final va face operația de `merge` pentru a-și publica ce a facut la poveste.

## Git, pe șleau:

Ei, bine, la fel cum Gitță gestionează schimbarile care se intamplă in scenariu, Git gestioneaza schimbarile care se intampla in folderul proiectului nostru. Fiecare modificare de linie este percepută ca o schimbare.

Atat Ana, Bogdan cat si Catalina, se duc pe `branch`-ul initial, si isi fac propriul `branch`.

Fiecare lucreaza la scenariu in paralel.

La final, fiecare incearca să își `merge`-uiasca modificarile. Prima persoana care face asta cumva se scapa de griji, pentru ca `branch`-ul initial nu s-a modificat. Odata ce primul merge se intampla, acum branch-ul initial este modificat.

Restul persoanelor au acum extra munca de a avea grija ca schimbarile sa fie consistente cu ce au facut cei dinaintea lor.

That is the beauty of it. 