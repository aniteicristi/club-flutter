# Widget-uri. Componenta de baza

Dupa cum discutasem si in celelalte cursuri, widget-uirle sunt componentele de baza, piesele de lego elementare pe care le putem folosi ca sa ne creem aplicatii. In continuare ne vom uitaa la cea mai simpla aplicatie in flutter si ce contine:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(const App());
}

class App extends StatelessWidget {
  const App({super.key});

  @override
  Widget build(BuildContext context) {
    return const MaterialApp(
      home: Scaffold(
        body: Text('hello'),
      ),
    );
  }
}

```

> ✨ Codul este disponibil pe dart-pad sa urmariti impreuna cu mine [aici](https://dartpad.dev/?id=d28b14883cff40309477b723ed1fa9f7)

Observam ca aplicatia noastra este ea in sine un widget `App` care are o functie build unde ne desfasuram interfata.

Primul widget pe care il vedem este MaterialApp. Acest widget reprezeinta aplicatia noastra propriuzisa, iar despre functionalitatile lui vom studia atunci cand invatam despre navigare. Ideea este ca fiecare widget pe care il folosim trebuie sa vina in `MaterialApp()`.

All doilea widget din nou nu e cunoscut, dar observam ca e pasat la `MaterialApp()` prin parametrul `home` foarte similar de felul in care pasam parametrii numiti la functii. Acest widget se numeste `Scaffold()`. Un scaffold reprezinta o pagina pe care o vedem in aplicatie. Prin pagina ne referim la un background asupra caruia putem sa punem alte widget-uri, cum ar fi acel `Text()`. 

Ok, dar ne trebuie si o aplicatie, si o pagina??? De ce trebuie sa folosim atatea ca sa afisam un simplu text pe ecran?

Pai, putem sa ne gandim la urmatorul lucru: O aplicatie poate sa aiba mai multe pagini. De exemplu cand stai pe instagram, ai lista de mesaje si cand dai click pe un mesaj te duce pe alta unde poti sa povestesti cu prietenii tai. Conceptul acesta de pagina este de baza cand vine vorba de aplicatii de mobil, si vom vedea mai multe despre el mai tarziu.

Observam ca `Scaffold()` nu are un `child`, ci un `body`. Daca ati mai facut o pagina web, poate va mai amintiti ca un html are doua taguri de baza, head si body. Well, si in flutter este similar, chiar daca doar in nume.

In acest caz simplist, noi afisam un text. Dar noi vrem aplicatii mai complexe de atat, care au mai multe elemente. Cu toate acestea, body ia un singur parametru. Ce ne facem?

## Column, Row și Stack

Aceste widget-uri sunt *widget-uri de layout*. Ce inseamna asta? Inseamna ca le putem folosi impreuna ca sa creem interfata noastra. Hai sa ne facem aplicatia unpic mai complexa:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(const App());
}

class App extends StatelessWidget {
  const App({super.key});

  @override
  Widget build(BuildContext context) {
    return const MaterialApp(
      home: Scaffold(
        body: Column(
          children: [
            Text('Title'),
            Text('Subtitle'),
            Text('Content content content content'),
          ],
        ),
      ),
    );
  }
}

```
Observam ca avem mai mult content, care este situat intr-o coloana pe ecranul nostru. Widget-ul `Column()` va lua ca argumente in `children` o lista de widget-uri specificate de noi. 

Desigur, am putea sa schimbam in loc de coloana sa fie rand si atunci elementele ar fi situate pe orizontala. Partea faina este ca noi putem sa punem orice widget in lista aceea de elemente, inclusiv un alt widget de tip `Column()`. Desigur, daca folosim doua coloane una in alta, nu facem nimic. O aplicatie mai comuna a acestui concept este sa punem un rand in coloana, ca sa avem mai multe elemente la finalul listei ordonate pe orizontala unul dupa altul:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(const App());
}

class App extends StatelessWidget {
  const App({super.key});

  @override
  Widget build(BuildContext context) {
    return const MaterialApp(
      home: Scaffold(
        body: Column(
          children: [
            Text('Title'),
            Text('Subtitle'),
            Text('Content content content content'),
            Row(
              children: [
                Icon(Icons.home),
                Icon(Icons.square),
                Icon(Icons.settings),
              ],
            ),
          ],
        ),
      ),
    );
  }
}

```

Hopa... un nou widget a intrat in cladire. Putem sa folosim widget-ul `Icon()` ca sa reprezentam o iconitia sugestiva. Primul argument al acestui widget este o vaoloare de tipul `IconData` care este defapt doar o colectie de diferite iconite pe care le putem folosi in aplicatiile noastre. Daca intrati pe [api.flutter.dev](https://api.flutter.dev/flutter/material/Icons-class.html) veti vedea o lista completa cu toate iconitele pe care le puteti folosi in aplicatiile voastre flutter. Daca aveti nevoie de iconite noi, acela pot fi create si importante in aplicatie.

Observam ca de cand am introdus randul, textul nostru este centrat pe pagina. De ce? In comportamentul default al `Column()` si `Row()` este sa se extinda pana cand nu mai pot pe axa lor principala (verticala pentru coloana si orizontala pentru rand). Cand era doar o coloana, aceasta se extindea pe toata aplicatia pana jos, dar pe axa transversala (cross axis) se extindea doar ca sa incapa textul. O data ce am introdus un rand, acesta a dorit sa se extinda pana la capat pe axa orizontala, iar impreuna cu el a tras textul la mijloc, deoarece coloana isi alineaza textul la mijloc ca comportament standard. Putem sa schimbam orientarea prin a ne juca cu `mainAxisAlignment` si `crossAxisAlignment`.

`Stack()` functioneaza similar cu row si column, doar ca isi pune elementele unul peste altul in interfata.

## Spatiere: Padding, Spacer

Alte trei widgeturi super importante cand vrem sa creem unpic de spatiere sunt cele mentionate in titlu.

`Padding()` este un widget care o data ce este inconjurat in jurul altui widget, va crea o spatiere in jurul lui in cele 4 directii: `top`, `bottom`, `left` si `right`. Aceasta spatiere este specificata folosind clasa de `EdgeInsets`, care specifica distanta in pixeli in fiecare directie. EdgeInsets are mai multe forme:

- `EdgeInsets.all(5.0)` - Adauga o spatiere de 5 pixeli in toate directiile.
- `EdgeInsets.symmetric(horizontal: 5, vertical: 2)` - Adauga o spatiere egala pe cele doua axe: sus si jos de 2 pixeli, dreapta si stanga de 5 pixeli.
- `EdgeInsets.only(left: 3, right:4, top:1)` - Adauga o spatiere specificata in fiecare directie in jurul widget-ului. daca nu e specificata pentru o directie, se asuma 0.

Haideti sa adaugam un padding la titlu:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(const App());
}

class App extends StatelessWidget {
  const App({super.key});

  @override
  Widget build(BuildContext context) {
    return const MaterialApp(
      home: Scaffold(
        body: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            Padding(
              padding: EdgeInsets.only(bottom: 8.0, left: 4.0),
              child: Text('Title'),
            ),
            Text('Subtitle'),
            Text('Content content content content'),
            Row(
              children: [
                Icon(Icons.home),
                Icon(Icons.square),
                Icon(Icons.settings),
              ],
            ),
          ],
        ),
      ),
    );
  }
}
```

Observam ca acum exista o distanta intre titlu si subtitlu. Acest widget e foarte folosit, deoarece cand ai de exemplu postari intr-o lista, trebuie sa pui o distanta intre acestea ca sa nu arate straniu.


Bun, dar daca am vrea ca acele iconite sa fie in josul paginii? In acest caz putem folosi un `Spacer()` care odata pus intr-o coloana sau un rand, va impinge toate elementele din inaintea lui intr-o parte, si celelalte in cealalta. Puteti sa va ganditi la el ca la un arc care e pus intre un rand de carti. Arcul se va extinde cat de tare poate pana cand cartile vor fi lipite una de alta si de perete.

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(const App());
}

class App extends StatelessWidget {
  const App({super.key});

  @override
  Widget build(BuildContext context) {
    return const MaterialApp(
      home: Scaffold(
        body: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            Padding(
              padding: EdgeInsets.only(bottom: 8.0, left: 1.0),
              child: Text('Title'),
            ),
            Text('Subtitle'),
            Text('Content content content content'),
            Spacer(),
            Row(
              children: [
                Icon(Icons.home),
                Icon(Icons.square),
                Icon(Icons.settings),
              ],
            ),
          ],
        ),
      ),
    );
  }
}
```

## Containere si Card-uri.

Bun, sa spunem ca am vrea totusi in aplicatia noastra sa avem un patrat portocaliu. Ca sa creem un patrat putem sa ne folosim de un container. `Container()` este un widget care deseneaza un patrat pe interfata. Desigur, acest patrat poate sa fie si rotunjit pana arata ca un cerc, dar asta este peste ce vrem sa facem astazi.

Haideti sa ne uitam peste urmatorul exemplu:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(const App());
}

class App extends StatelessWidget {
  const App({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        body: Row(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            Container(
              width: 100,
              height: 200,
              color: Colors.red,
            ),
            Container(
              width: 100,
              height: 200,
              color: Colors.yellow,
            ),
            Container(
              width: 100,
              height: 200,
              color: Colors.blue,
            ),
          ],
        ),
      ),
    );
  }
}
```

> ✨ Codul este disponibil pe dart-pad sa urmariti impreuna cu mine [aici](https://dartpad.dev/?id=0fffd97db6b90e0fe6e5e986f935c2d6)

Observam aici un steag care ni se pare cunoscut. Un container este defapt un widget care are mai multe functionalitati care se regasesc si in alte widget-uri. De exemplu, width si height se gasesc si in `SizedBox()`, dar color nu.

Daca setam diferite valori pentru width, putem sa variem lucrurile.

Fiecare container poate sa aiba inautru lui alte widget-uri, trebuie doar sa specificam care mai exact:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(const App());
}

class App extends StatelessWidget {
  const App({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        body: Row(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            Container(
              width: 100,
              height: 200,
              color: Colors.red,
              child: Text('Moldova'),
            ),
            Container(
              width: 100,
              height: 200,
              color: Colors.yellow,
              child: Text('Valahia'),

            ),
            Container(
              width: 100,
              height: 200,
              color: Colors.blue,
              child: Text('Transilvania'),

            ),
          ],
        ),
      ),
    );
  }
}
```

Un container are si proprietatile de `margin` si `padding` care pot fi specificate cu un obiect de tip `EdgeInsets`. Care este diferenta dintre margin si padding? Pai spatierea de margin se aplica inafara containerului, in timp ce cea de padding se aplica inauntru containerului (practic se aplica pe copilul containerului.)

Dar daca am dori sa sugeram utilizatorului ca un obiect este "deasupra" altui obiect? In aceste cazuri ne folosim de widget-ul `Card()` care va aplica o umbra asupra copilului sau, practic ridicandul vizual dintre celelalte:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(const App());
}

class App extends StatelessWidget {
  const App({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        body: Row(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            Container(
              width: 100,
              height: 200,
              color: Colors.red,
              child: Text('Moldova'),
              margin: EdgeInsets.symmetric(horizontal: 10),
            ),
            Card(
              child: Container(
                width: 100,
                height: 200,
                color: Colors.yellow,
                child: Text('Valahia'),
                margin: EdgeInsets.symmetric(horizontal: 10),
              ),
            ),
            Container(
              width: 100,
              height: 200,
              color: Colors.blue,
              child: Text('Transilvania'),
              margin: EdgeInsets.symmetric(horizontal: 10),
            ),
          ],
        ),
      ),
    );
  }
}
```

Ca sa schimbam cat de "deasupra" este obiectul, putem sa modificam optiunea de `elevation`. Observam ca din cauza margini containerului, avem un spatiu alb liber. Haide-ti sa scoatem marginea de pe container.

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(const App());
}

class App extends StatelessWidget {
  const App({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        body: Row(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            Container(
              width: 100,
              height: 200,
              color: Colors.red,
              child: Text('Moldova'),
              margin: EdgeInsets.symmetric(horizontal: 10),
            ),
            Card(
              elevation: 12,
              child: Container(
                width: 100,
                height: 200,
                color: Colors.yellow,
                child: Text('Valahia'),
              ),
            ),
            Container(
              width: 100,
              height: 200,
              color: Colors.blue,
              child: Text('Transilvania'),
              margin: EdgeInsets.symmetric(horizontal: 10),
            ),
          ],
        ),
      ),
    );
  }
}
```

## Expanded

Expanded este un widget extrem de folositor cand vrem sa ne jucam mai in detaliu cu dispunerea widget-urilor. Cand inconjuram un widget in `Expanded()` ii spunem defapt sa incerce sa ocupe tot spatiul pana nu mai poate. 

Un expanded este foarte similar cu un spacer, ba chiar daca un expanded nu are un `child` specificat, se comporta **exact** ca `Spacer()`.

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(const App());
}

class App extends StatelessWidget {
  const App({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        body: Row(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            Expanded(
              child: Container(
              width: 100,
              height: 200,
              color: Colors.red,
              child: Text('Moldova'),
              margin: EdgeInsets.symmetric(horizontal: 10),
            ),
            ),
            Card(
              elevation: 12,
              child: Container(
                width: 100,
                height: 200,
                color: Colors.yellow,
                child: Text('Valahia'),
              ),
            ),
            Container(
              width: 100,
              height: 200,
              color: Colors.blue,
              child: Text('Transilvania'),
              margin: EdgeInsets.symmetric(horizontal: 10),
            ),
          ],
        ),
      ),
    );
  }
}
```

> 🔥 **Important!** - Expanded se poate folosi doar inauntru la `Column()` si `Row()`.

Dar intrebarea este ce se intampla daca punem toate widget-urile in expanded?

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(const App());
}

class App extends StatelessWidget {
  const App({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        body: Row(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            Expanded(
              child: Container(
              width: 100,
              height: 200,
              color: Colors.red,
              child: Text('Moldova'),
              margin: EdgeInsets.symmetric(horizontal: 10),
            ),
            ),
            Expanded(
              child: Card(
                elevation: 12,
                child: Container(
                  width: 100,
                  height: 200,
                  color: Colors.yellow,
                  child: Text('Valahia'),
                ),
              ),
            ),
            Expanded(
              child: Container(
                width: 100,
                height: 200,
                color: Colors.blue,
                child: Text('Transilvania'),
                margin: EdgeInsets.symmetric(horizontal: 10),
              ),
            ),
          ],
        ),
      ),
    );
  }
}
```

Pai, fiecare va incerca sa se extinda la fel de tare, si vor ocupa tot spatiul, impartind-ul in 3 parti egale.

Bun, dar daca de exemplu, transilvania e mai tare decat celelalte doua regate, si am vrea sa ocupe mai mult spatiu in steag. Expanded are o proprietate numita: `flex`, care nespecificata este initializata la 1. Acest flex semnifica partea din spatiul total pe care o poate ocupa. Deci daca am pune un flex de 3 in expanded-ul translivaniei, atunci transilvania ar ocupa 3 din 5 parti din spatiu (unde celelalte doua regate ocupa impreuna 2/5).

```dart

import 'package:flutter/material.dart';

void main() {
  runApp(const App());
}

class App extends StatelessWidget {
  const App({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        body: Row(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            Expanded(
              child: Container(
              width: 100,
              height: 200,
              color: Colors.red,
              child: Text('Moldova'),
              margin: EdgeInsets.symmetric(horizontal: 10),
            ),
            ),
            Expanded(
              child: Card(
                elevation: 12,
                child: Container(
                  width: 100,
                  height: 200,
                  color: Colors.yellow,
                  child: Text('Valahia'),
                ),
              ),
            ),
            Expanded(
              flex: 3,
              child: Container(
                width: 100,
                height: 200,
                color: Colors.blue,
                child: Text('Transilvania'),
                margin: EdgeInsets.symmetric(horizontal: 10),
              ),
            ),
          ],
        ),
      ),
    );
  }
}
```

Desigur, daca am vrea ca moldova sa aiba un flex de 2, atunci ea ar fi mai mare decat valahia, dar mai mica ca transilvania. Totalul de spatiu este mereu fiecare flex adunat, caz in care ar veni 2 + 1 + 3 = 6, deci transilvania ar ocupa 3 sesimi, moldova 2 sesimi, si valahia 1 sesime din spatiul total.

Observati cat de puternic este acest mecanism ca sa specificam orice fel de aliniere si dispunere de care avem nevoie.

