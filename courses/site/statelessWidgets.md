# Widget-uri. Componenta de baza

După cum discutaserăm și în celelalte cursuri, widget-urile sunt componentele de bază, piesele de lego elementare pe care le putem folosi ca să ne creăm aplicații. În continuare, ne vom uita la cea mai simplă aplicație în Flutter și ce conține:

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

> ✨ Codul este disponibil pe dart-pad să urmăriți împreună cu mine [aici](https://dartpad.dev/?id=d28b14883cff40309477b723ed1fa9f7)

Observăm că aplicația noastră este ea în sine un widget `App` care are o funcție build unde ne desfășurăm interfața.

Primul widget pe care îl vedem este `MaterialApp`. Acest widget reprezintă aplicația noastră propriu-zisă, iar despre funcționalitățile lui vom studia atunci când învățăm despre navigare. Ideea este că fiecare widget pe care îl folosim trebuie să vină în `MaterialApp()`.

Al doilea widget, deși nu e cunoscut, este pasat la `MaterialApp()` prin parametrul `home`, foarte similar cu modul în care pasăm parametri numiți la funcții. Acest widget se numește `Scaffold()`. Un scaffold reprezintă o pagină pe care o vedem în aplicație. Prin pagină ne referim la un background asupra căruia putem să punem alte widget-uri, cum ar fi acel `Text()`.

Ok, dar ne trebuie și o aplicație, și o pagină??? De ce trebuie să folosim atâtea pentru a afișa un simplu text pe ecran?

Pai, putem să ne gândim la următorul lucru: O aplicație poate să aibă mai multe pagini. De exemplu, când stai pe Instagram, ai lista de mesaje și când dai click pe un mesaj te duce pe altă pagină unde poți să povestești cu prietenii tăi. Conceptul acesta de pagină este de bază când vine vorba de aplicații de mobil, și vom vedea mai multe despre el mai târziu.

Observăm că `Scaffold()` nu are un `child`, ci un `body`. Dacă ați mai făcut o pagină web, poate vă mai amintiți că un HTML are două taguri de bază, `head` și `body`. Ei bine, și în Flutter este similar, chiar dacă doar în nume.

În acest caz simplist, noi afișăm un text. Dar noi vrem aplicații mai complexe de atât, care au mai multe elemente. Cu toate acestea, `body` ia un singur parametru. Ce ne facem?

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
Observăm că avem mai mult conținut, care este situat într-o coloană pe ecranul nostru. Widget-ul `Column()` va lua ca argumente în `children` o listă de widget-uri specificate de noi.

Desigur, am putea să schimbăm în loc de coloană să fie un rând și atunci elementele ar fi situate pe orizontală. Partea faină este că noi putem să punem orice widget în lista aceea de elemente, inclusiv un alt widget de tip `Column()`. Desigur, dacă folosim două coloane una în alta, nu facem nimic. O aplicație mai comună a acestui concept este să punem un rând în coloană, ca să avem mai multe elemente la finalul listei ordonate pe orizontală unul după altul:

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

Hopa... un nou widget a intrat în clădire. Putem să folosim widget-ul `Icon()` ca să reprezentăm o iconiță sugestivă. Primul argument al acestui widget este o valoare de tipul `IconData`, care este de fapt doar o colecție de diferite iconițe pe care le putem folosi în aplicațiile noastre. Dacă intrați pe [api.flutter.dev](https://api.flutter.dev/flutter/material/Icons-class.html), veți vedea o listă completă cu toate iconițele pe care le puteți folosi în aplicațiile voastre Flutter. Dacă aveți nevoie de iconițe noi, acelea pot fi create și importate în aplicație.

Observăm că de când am introdus rândul, textul nostru este centrat pe pagină. De ce? În comportamentul implicit al `Column()` și `Row()`, este să se extindă până când nu mai pot pe axa lor principală (verticală pentru coloană și orizontală pentru rând). Când era doar o coloană, aceasta se extindea pe toată aplicația până jos, dar pe axa transversală (cross axis) se extindea doar ca să încapă textul. Odată ce am introdus un rând, acesta a dorit să se extindă până la capăt pe axa orizontală, iar împreună cu el a tras textul la mijloc, deoarece coloana își aliniază textul la mijloc ca comportament standard. Putem să schimbăm orientarea prin a ne juca cu `mainAxisAlignment` și `crossAxisAlignment`.

`Stack()` funcționează similar cu row și column, doar că își pune elementele unul peste altul în interfață.

## Spațiere: Padding, Spacer

Alte două widget-uri super importante când vrem să creăm un pic de spațiu sunt cele menționate în titlu.

`Padding()` este un widget care, odată ce este înconjurat în jurul altui widget, va crea un spațiu în jurul lui în cele 4 direcții: `top`, `bottom`, `left` și `right`. Acest spațiu este specificat folosind clasa `EdgeInsets`, care specifică distanța în pixeli în fiecare direcție. `EdgeInsets` are mai multe forme:

- `EdgeInsets.all(5.0)` - Adaugă un spațiu de 5 pixeli în toate direcțiile.
- `EdgeInsets.symmetric(horizontal: 5, vertical: 2)` - Adaugă un spațiu egal pe cele două axe: sus și jos de 2 pixeli, dreapta și stânga de 5 pixeli.
- `EdgeInsets.only(left: 3, right: 4, top: 1)` - Adaugă un spațiu specificat în fiecare direcție în jurul widget-ului. Dacă nu este specificat pentru o direcție, se asumă 0.

Haideți să adăugăm un padding la titlu:

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

Observăm că acum există o distanță între titlu și subtitlu. Acest widget este foarte folosit, deoarece când ai, de exemplu, postări într-o listă, trebuie să pui o distanță între acestea ca să nu arate ciudat.

<!-- introduce an example with padding vs without padding-->

Bun, dar dacă am vrea ca acele iconițe să fie în josul paginii? În acest caz, putem folosi un `Spacer()` care odată pus într-o coloană sau un rând, va împinge toate elementele dinaintea lui într-o parte, și celelalte în cealaltă. Puteți să vă gândiți la el ca la un arc care este pus între un rând de cărți. Arcul se va extinde cât de tare poate până când cărțile vor fi lipite una de alta și de perete.

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

## Containere și Card-uri.

Bun, să spunem că am vrea totuși în aplicația noastră să avem un pătrat portocaliu. Ca să creăm un pătrat, putem să ne folosim de un container. `Container()` este un widget care desenează un pătrat pe interfață. Desigur, acest pătrat poate să fie și rotunjit până arată ca un cerc, dar asta este peste ce vrem să facem astăzi.

Haideți să ne uităm peste următorul exemplu:

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

> ✨ Codul este disponibil pe dart-pad să urmăriți împreună cu mine [aici](https://dartpad.dev/?id=0fffd97db6b90e0fe6e5e986f935c2d6)

Observăm aici un steag care ni se pare cunoscut. Un container este de fapt un widget care are mai multe funcționalități care se regăsesc și în alte widget-uri. De exemplu, `width` și `height` se găsesc și în `SizedBox()`, dar `color` nu.

Dacă setăm diferite valori pentru `width`, putem să variem lucrurile.

Fiecare container poate să aibă în interiorul lui alte widget-uri, trebuie doar să specificăm care mai exact:

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

Un container are și proprietățile `margin` și `padding` care pot fi specificate cu un obiect de tip `EdgeInsets`. Care este diferența dintre margin și padding? Pai spatierea de margin se aplică în afara containerului, în timp ce cea de padding se aplică înăuntru containerului (practic se aplică pe copilul containerului).

Dar dacă am dori să sugerăm utilizatorului că un obiect este "deasupra" altui obiect? În aceste cazuri ne folosim de widget-ul `Card()` care va aplica o umbră asupra copilului sau, practic ridicându-l vizual dintre celelalte:

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

Ca să schimbăm cât de "deasupra" este obiectul, putem să modificăm opțiunea de `elevation`. Observăm că din cauza marginii containerului, avem un spațiu alb liber. Haideți să scoatem marginea de pe container.

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

`Expanded()` este un widget extrem de folositor când vrem să ne jucăm mai în detaliu cu dispunerea widget-urilor. Când înconjurăm un widget în `Expanded()`, îi spunem de fapt să încerce să ocupe tot spațiul până nu mai poate.

Un `Expanded()` este foarte similar cu un `Spacer`, ba chiar dacă un `Expanded` nu are un `child` specificat, se comportă **exact** ca `Spacer()`.

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

> 🔥 **Important!** - `Expanded` se poate folosi doar înăuntru la `Column()` și `Row()`.

Dar întrebarea este ce se întâmplă dacă punem toate widget-urile în `Expanded`?

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

Pai, fiecare va încerca să se extindă la fel de tare și vor ocupa tot spațiul, împărțindu-l în 3 părți egale.

Dar, dacă de exemplu, Transilvania e mai importantă decât celelalte două regate, și am vrea să ocupe mai mult spațiu în steag. `Expanded` are o proprietate numită: `flex`, care, nespecificată, este inițializată la 1. Acest flex semnifică partea din spațiul total pe care o poate ocupa. Deci, dacă am pune un flex de 3 în `Expanded`-ul Transilvaniei, atunci Transilvania ar ocupa 3 din 5 părți din spațiu (unde celelalte două regate ocupă împreună 2/5).

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

Desigur, dacă am vrea ca Moldova să aibă un flex de 2, atunci ea ar fi mai mare decât Valahia, dar mai mică decât Transilvania. Totalul de spațiu este mereu fiecare flex adunat, caz în care ar veni 2 + 1 + 3 = 6, deci Transilvania ar ocupa 3 șesimi, Moldova 2 șesimi, și Valahia 1 șesime din spațiul total.

Observați cât de puternic este acest mecanism pentru a specifica orice fel de aliniere și dispunere de care avem nevoie.

## ListView și prietenii
Dacă se poate spune un lucru despre aplicațiile mobile este următorul:

> "În general, majoritatea aplicațiilor mobile pot fi reduse la o listă de chestii."

Hai să luăm câteva exemple bune:

- Instagram: o listă de postări
- TikTok: o listă de videoclipuri
- YouTube: o listă de videoclipuri. Dai click pe un videoclip ai o listă de recomandări și o listă de comentarii.
- Spotify: o listă de cântece

Și putem să continuăm tot așa. Lista de contacte, lista de mâncare de comandat, etc... Exemplele sunt nelimitate.

De aceea, cei deștepți care au creat Flutter au văzut că este nevoie de un widget special care să reprezinte o listă, așa că au inventat `ListView()`.

Hai să luăm codul inițial și să folosim un `ListView()` în loc de un `Column()`:

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
        body: ListView(
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
Observăm că și `ListView` are copii și că până acum se comportă exact ca și `Column`. Există totuși o diferență. Hai să rulăm următorul cod:


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
        body: ListView(
          children: [
            for (int i in List.generate(100, (index) => index))
              Text("Element is the $i'th in a list"),
          ],
        ),
      ),
    );
  }
}
```
Ce am făcut aici este că am generat 100 de widget-uri `Text()` folosind un for într-o listă generată 100 de elemente de tip întreg care sunt numere crescătoare de la 0 până la 99. Observăm că toate aceste elemente ne ies de pe ecran. Când ele sunt plasate într-o coloană, acea coloană va arunca o eroare și se va plânge că nu are destul loc ca să-și afișeze copii, în timp ce ListView()-ul e based and scroll-pilled. Dacă îi dai prea multe elemente, el zice: no, uite că poți să dai scroll prin ele și nu se plânge că nu are loc.

Însă, la fel ca și coloana, list-view-ul se va extinde până când nu mai poate, deci dacă bagăm un list-view într-o coloană, Flutter va plânge lacrimi amare pentru că nu va cum să afișeze așa ceva pe ecran și îți va da o eroare.

Pe lângă faptul că poate să aibă mai multe elemente în el, sub capotă, ListView() este mult mai optimizat pentru liste colosale, deci și dacă aveți 1000 de elemente, acest widget se va descurca fără să ne facă prea mult lag. În schimb, coloana ar ceda mult mai repede și FPS-urile aplicației noastre ar scădea dramatic.

### ListTile

ListTile este un widget care a fost creeat sa arate bine intr-un listview. El ar putea sa fie numit un element intr-o lista si vine preconfigurat cu padding, separator si cu diverse optiuni ca sa ne dea voie sa 