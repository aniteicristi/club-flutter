## Care este treaba cu flutter?

### Lego

Probabil ati auzit sau ati vazut in magazine acest tip de jucarie. Lego este un set de piese care vine dezasamblat iar scopul jucăriei este să il asamblezi conform instructiunilor date. 

Piesele in sine sunt foarte simple si neinteresante, dar daca le combini in felul in care trebuie poti sa obti orice iti doresti, fie un dinozaur, fie o masina etc...

Iar partea cea mai tare este ca poti sa nu respecti instructiunile. Poti sa construiesti ce vrei, atata timp cat ai toate piesele potrivite.

![Lego](img/lego.jpeg)

### Filozofia Flutter

Flutter este foarte asemanator cu lego. La fel ca si piesele simple care vin intr-un set de lego, flutter iti pune la dispozitie niste piese simple care se pot intrelega pentru a produce interfete complexe si extraordinar de frumoase.

Daca ne uitam la orice interfata de aplicatie de mobil, putem sa observam ca unele elemente pot fi grupate impreuna, dupa cum vedem in exemplul de mai jos.

![YT Music](img/yt_music_1.png)

Putem sa observam pe acest ecran daca ne uitam mai indeaproape ca interfata este defapt impartita in mici elemente care sunt aranjate impreuna. 

- Topbar-ul e impartit in 3 iconite si un tab-bar care sunt aranjate intr-un rand.
- Titlul este format dintr-un text si 2 iconite aranjate intr-un rand.
- Control bar-ul este creat dintr-un rand de butoane de diferite dimensiuni si cu diferite iconite aranjate intr-un rand.

Ideea e ca putem face aceasta impartire la nivele diferite. Putem sa impartim pe elemente, iar impreuna, aceste elemente creeaza o sub-grupare, cum sunt topbar-ul, titlul, control-bar-ul sau navigation bar.

Doar ca, *și asta este șmecheria*, la randul lor, aceste grupuri de elemente pot fi considerate si ele elemente.

Asa ca putem spune ca interfata noastră e formata din topbar, imagine, titlu, artist, progres, control bar si navigation bar, toate aranjate intr-o coloana.

Daca stim sa compunem aceste elemente si să le aranjam in coloane sau randuri (sau una peste alta :wink:), putem sa cream orice interfata pe care ne-o putem imagina.

> "Ok. Ok. Dar eu nu stiu sa creez o imagine sau o iconita, sau un buton. Ce fac?"

Ne intoarcem la prima analogie. Cand construim lego, nu incepem de la zero. Nu știm să modelăm plastic încins. Dar nici nu trebuie. Toate piesele de care avem nevoie vin in pachet, standardizate și gata de construit. :smile:


## Ce este un Widget?

Un widget este un element in interfata. Este un concept destul de abstract. Un widget poate sa fie un buton, un text, o iconita sau multe alte elemente care care apar pe ecranul telefonului.

Doar ca, un widget poate sa fie si un element abstract care este invizibil pe ecranul telefonului, dar care are rolul de a aranja alte widget-uri intr-un anumit mod (de exemplu rand sau coloana), sau care introduc un anumit comportament. (De exemplu `SafeArea()`)

Rolul nostru ca programatori este sa ne folosim de aceste Widget-uri pentru a descrie interfetele pe care le dorim. Haide sa disecam exact cum arata unul dintre cele mai simple widget-uri in codul nostru:

```dart
Container(
  height: 20,
  width: 20,
  child: Text("Hello");
);

```

Observam ca un widget are un nume, urmat de doua paranteze `Container()`. Inauntrul acestor paranteze observam mai mullte perechi de proprietati si valori, separate de catre o virgula `,`.

Fiecare widget are un set de proprietati diferit. Acestea sunt configurate prin faptul ca le mentionam numele, urmat de doua puncte si de proprietatea asta. Aceste proprietati pot sa fie intregi `int` sau numere cu virgula flotanta `float` sau `double`. Pot să fie chiar șiruri de caractere `String`, iar cel mai important:

**In lista de proprietati ale unui widget exista argumentul `child` sau `children` care primeste un alt widget sau o lista de alte widget-uri.**

> In cazul unor widget-uri cum ar fi `Text()` prima proprietate nu are nume. Acea proprietate este unnamed si e pusa mereu la inceputul listei de proprietati.

Folosind aceste proprietati de tip child noi putem sa combinam widget-uri in orice mod. proprietatile child pot sa ia orice widget. Ca sa enumeram cateva widget-uri avem:

- `Text()` - arata un text pe ecran.
- `Icon()` - deseneaza o iconita pe ecran. 
- `Container()` - creeaza un container cu o anumita inaltime / latime. Containerul este invizibil daca nu modificam culoarea
- `Row()` - aranjeaza widget-urile din lista de `children` intr-un rand.
- `Column()` - aranjeaza widget-urile din lista de `children` intr-o coloana.
- `Center()` - centreaza widgetul specificat in proprietatea `child`

## Exerciții

Unde vedeti comentarii cu todo (// TODO: ), rezolvati problemele. 

[dartpad](https://dartpad.dev/?id=a3114e34db0ff9d74d2dffabdf723013 ':include :type=iframe width=100% height=800px loading="lazy"')

