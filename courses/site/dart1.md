# Dart

## Ce este dart?

Dart este limbajul în care noi scriem aplicațiile. E de notat că Dart este diferit de Flutter. Dart a apărut ca limbaj înaintea lui Flutter. Putem să ne gândim că dacă Flutter este setul de Lego, Dart este design-ul distinctiv al bucăților de Lego, cum ar fi diferitele conectoare de pe fiecare piesă.

Atunci Flutter ce este? Un framework. Adică un set de cod predefinit (scris în Dart) care simplifică dezvoltarea de aplicații mobile/web/desktop în feluri pe care le vom explora mai în detaliu în cursurile viitoare.

Dart este un limbaj care în multe privințe este asemănător cu C++ și în multe altele este destul de diferit, însă multe concepte vor părea familiare.

Haidem să ne uităm la cel mai simplu program în Dart:

```dart
void main(){
  print('Hello World');
}

```

Observăm că la fel ca și în C++, avem o funcție main. De aici se execută codul nostru în Dart. Ca să rulăm, nu avem nevoie să #include nimic, și nici nu avem nevoie de using namespace std;.

Pentru a scrie ceva în consolă, folosim funcția print. Observăm că șirurile de caractere nu sunt delimitate cu "" (ghilimele), ci cu '' (apostroafe). Însă ambele delimitări se acceptă. Codul de jos are același efect:

```dart
void main(){
  print("Hello World");
}
```

## Variabile în Dart

Putem să declarăm o variabilă în mai multe moduri:

```dart
void main(){
  var a = 1;
  int b = 1;
}
```

Care este diferența?

- Variabila `a` este declarată cu cuvântul-cheie `var`. Acest cuvânt-cheie declară o variabilă fără un tip explicit (cum ar fi `int` sau `double`). Acest tip va fi înțeles de către Dart ca fiind `int`, pentru că i-am atribuit valoarea 1.
- Variabila `b` este declarată exact ca în C/C++. Nimic ieșit din comun.


## Tipuri de bază în Dart

### `int`
La fel ca și în C++, un întreg este reprezentat prin `int` și declarat exact ca în C++.

```dart
void main(){
  int a, b, c = 0;
  b = 1;
  a = b + c;
}
```

Ce este important de știut este că întregii nu se auto-initializează la 0 când sunt declarați în `main`. Dacă, de exemplu, urma să folosim `a` înainte să fie atribuit, în C++ era ok și nu se supăra nimeni, în Dart veți întâmpina o eroare care spune ceva de genul "non-nullable variable must be initialized before first use." Fiți responsabili cu variabilele voastre!

> 💡 `int`-ul se folosește exact ca în C++, dar dacă doriți să împărțiți două `int`-uri folosind operatorul `/`, rezultatul va fi mereu un `double`. Pentru împărțire cu rest, se folosește `~/`, dar acest concept nu este foarte important.

### `float/double`

La fel ca în C++, numerele reale (cu virgulă mobilă) sunt reprezentate de `float` și `double`. Cu precădere, `double` este folosit mai des, dar tot ce poți face cu unul poți face și cu celălalt, dar `double` suportă numere mai mari.

### `bool`

La fel ca în C++. Are două valori posibile: `true` sau `false`. Doar că diferit de C++, `false` nu este egal cu `0`. Este incorect să compari un număr cu un boolean.

### `String`

Unul dintre cele mai importante tipuri în Dart, string reprezintă un șir de caractere. Acest concept există în C++, dar s-ar putea să nu îl cunoașteți. Ideea este că în loc ca un șir de caractere să fie tratat ca un șir de `char`, acesta este tratat ca o variabilă de sine stătătoare care poate fi atribuită, modificată, etc...

```dart
void main() {
  String hello = "Hello World";

  hello = "goodbye";

  hello = hello + ", cruel world!";
  print(hello); // Afișează: "goodbye, cruel world!"
}
```

Ce este interesant este că în loc să folosim funcții precum `strcat` ca să concatenăm două șiruri de caractere, putem doar să folosim operatorul `+`. Cât de simplu!

Dacă întâmplător adăugați un punct după variabila string, veți fi întâmpinați cu o multitudine de metode pe care le puteți aplica. Cel mai simplu ar fi să vedem cum luăm lungimea unui string.

```dart
void main() {
  String hello = "Hello World!";
  //In C: strlen(hello);
  //In C++: hello.size();
  print(hello.length); // Prints: 12
}
```
În acest caz, `length` este un atribut al șirului de caractere.

Nu are neapărat rost să intrăm în toate aceste atribute, dar puteți să vedeți ce altceva puteți face cu un șir de caractere dacă vă uitați la acest tutorial: [link](https://api.flutter.dev/flutter/dart-core/String-class.html).

Desigur, dacă doriți să selectați fiecare caracter dintr-un șir de caractere, puteți să folosiți o sintaxă similară cu accesarea unui element dintr-un șir, dar acest lucru nu va fi atât de folosit când vom folosi Flutter.

Un alt concept extraordinar de folositor în Dart este interpolarea de șiruri de caractere. Interpolare? Hă?

Imaginați-vă că doriți să afișați un text de genul: "Ana are 5 mere și 8 portocale." Dar, ați vrea să afișați acest text în funcție de valoarea unor variabile din codul vostru. În C++, ați face ceva de genul acesta:

```C++
int mere = 5;
int portocale = 8;
cout << "Ana are " << mere << " mere si " << portocale << " portocale.\n"
```

În Dart nu avem `cout`, dar avem funcția `print` care ne afișează un șir de caractere și am putea să ne folosim de ideea de concatenare a șirurilor de caractere:

```dart
int mere = 5;
int portocale = 8;
String mesaj = "Ana are " + mere + " mere si " + portocale + " portocale.\n"; // NUUUU EROAREE
print(mesaj);
```

Acest cod va da eroare. De ce? `mere` este un `int`, deci nu poate fi concatenat cu un `String`. Putem să rezolvăm această problemă folosind funcția `toString()`, care este apelată pe `int`-uri.

```dart
int mere = 5;
int portocale = 8;
String mesaj = "Ana are " + mere.toString() + " mere si " + portocale.toString() + " portocale\n";
print(mesaj); // Prints: Ana are 5 mere si 8 portocale.
```

Ați obosit de la atâtea probleme? Eu da. Nu vreau să fac asta de fiecare dată când vreau să creez un șir de caractere dinamic. Noroc că dezvoltatorii Dart s-au gândit la acest aspect și au decretat:

'Thou shall use string interpolation!'

Interpolarea șirurilor de caractere constă în a îmbrăca variabile direct în textul șirului de caractere în următorul mod:


```dart
int mere = 5;
int portocale = 8;
String mesaj = "Ana are ${mere} mere si ${portocale} portocale.\n";
print(mesaj); // Prints: Ana are 5 mere si 8 portocale.
```

"Dacă scriem `${}` într-un șir de caractere, înăuntru putem să scriem orice variabilă între acolade, iar acea variabilă va fi convertită direct într-un șir de caractere. Fără sudoare și chiar mai flexibil decât `cout`, pentru că acum putem să folosim în continuare acel mesaj construit.

Ba chiar, înăuntrul acelor acolade putem să punem orice linie de cod care ne întoarce o valoare, deci poate cineva inspirat ar dori să facă ceva de genul:"

```dart
int mere = 5;
int portocale = 8;
String mesaj = "Ana are ${mere} mere si ${portocale} portocale. Are in total ${mere + portocale} fructe!\n";
print(mesaj); // Prints: Ana are 5 mere si 8 portocale. Are in total 14 fructe!
```

> 💡 Observați cum la finalul fiecărui șir de caractere am folosit `\n`. `endl` din C++ nu există în Dart. În schimb, folosim caracterul pentru pagină nouă `\n` (care există și în C/C++ 😉).

### `List`

Listele sunt echivalentul șirurilor în Dart, dar sunt un pic diferite față de șiruri. Diferențele nu sunt vizibile în mare parte pentru programatori, dar poate cei care au mai fost la olimpiadă pot să-mi spună diferența dintre un șir și o listă înlănțuită. Ideea este că listele în Dart se comportă ca și șiruri, dar sunt de fapt liste înlănțuite. Nu contează atât de mult dacă nu ne gândim la performanța aplicației noastre. Imaginați-vă că sunt șiruri de caractere.

Ce este interesant aici este că pentru a declara o listă, trebuie să specificăm și tipul de variabilă care se află în acea listă în felul urmator:

```dart
void main() {
  List<int> numere = [0, 1, 2, 3, 4];

  print(numere[0]) //Prints: 0
  print(numere[3]) //Prints: 3
  print(numere[10]) // OOOH NOOOO!
}
```

Observăm că atunci când vorbim de liste, de obicei elementele unei liste sunt specificate între paranteze drepte `[]` și sunt separate prin virgulă.

Ceea ce este diferit față de C++ este că nu trebuie să specificăm o lungime maximă pentru listă, dar dacă încercăm să accesăm un element de la o poziție care nu există, atunci programul va genera o eroare de indexare.

Bun, atunci cum aș inițializa o listă de, să zicem, 100 de șiruri de caractere? Există trei metode:

```dart
List<int> nume = [
  "Ana",
  "Marcel",
  "George",
  // ... Si tot asa pana la 100 de nume.
]
```

Sau

```dart
List<String> nume = List.filled(100, "", growable: true);
```

Sau

```dart
List<String> nume = []; // Empty list.

for(int i = 0; i < 100; i++){
  nume.add("");
}

```

Ok, am ajuns la partea de 'și în multe altele este destul de diferit de C++'.

- În prima metodă, putem să declarăm fiecare element explicit. Deși sună ca o metodă foarte proastă de a crea o listă de 100 de elemente (și este...), în programarea de zi cu zi în Flutter, această metodă de a crea o listă este cea mai des folosită. Imaginați-vă un `Row()` care are ca și `children` o listă de `Widget`-uri. Nu o să aibă 100 de copii, ci probabil cam 10 în general, în funcție de cât de complicată este interfața noastră.
- În a doua metodă, putem să folosim o funcție specială numită `List.filled()` (care se numește constructor, dar vom vedea ce înseamnă asta mai târziu) și care ia ca parametri lungimea listei și un element "implicit" cu care să umple lista. Parametrul `growable` este menționat în caz că vrem să mai adăugăm elemente la listă sau nu mai târziu.
- În a treia metodă, începem de la o listă goală, declarată cu paranteze pătrate: `[]`, și, folosind un `for` foarte familiar, pur și simplu adăugăm șirul de caractere `""` la coada listei de 100 de ori.

Aici s-ar putea să existe mai multe confuzii, dar în orice caz, aceste liste se comportă asemănător cu șirurile de caractere din C++. Hai să încercăm să parcurgem o listă și să afișăm elementele ei:

```dart
void main() {
  List<int> numere = [1,2,3,4,5];

  for(int i = 0; i < numere.length; i++) {
    print(numere[i]);
  }
}
```
Acest mod de parcurgere ar trebui să vă pară familiar. Cu toate acestea, acest mod de parcurgere are câteva dezavantaje:

- Trebuie să folosim acel index `i` ca să adresăm fiecare element în parte.
- Trebuie să apelăm `.length` ca să găsim lungimea listei.
- Nu este ușor de urmărit / lizibil.

Desigur, dacă avem nevoie de acel index, atunci este mai avantajos să parcurgem în felul acesta. În plus, în C, nu putem să facem ceva mai bun.

> În C++ avem `for(auto x : lista)`, dar probabil majoritatea nu știți exact despre ce vorbesc...

În Dart putem face mai bine:

```dart
void main() {
  List<int> numere = [1,2,3,4,5];

  for(int numar in numere){
    print(numar);
  }
}
```

În modul de mai sus, putem să parcurgem lista folosind variabila `numar`. Este foarte ușor de citit. Codul îți spune exact ce face: "Pentru fiecare `numar` în `numere`, fă ce este aici în paranteze." Este un mod mai bun, iar acest lucru se va arăta mai încolo.

## Condiții și Bucle

Condițiile și buclele funcționează exact ca în C/C++.

```dart
void main() {
  int a = 2;
  if(a == 2){
    print('ESTE!!!');
  }
  else {
    print('NU ESTE :<');
  }
}
```

```dart
void main(){
  while(true){
    print("computer go BRRRR!");
  }

  for(int i = 0; i < 1; i++){
    print("This loop should have been a statement. :<");
    break;
  }
}
```

> 💡 Observați că în general, când scriu cod, pun acolada fix după condiție/instrucțiune/funcție. Acesta este stilul prestabilit în Dart. Poate să fie ciudat la început, dar vă economisește o grămadă de spațiu pe ecran.

## Funcții

Pentru a declara și a folosi funcții în Dart, facem lucruri foarte similare cu C/C++. Până la urmă, am făcut asta de mai multe ori cu funcția `main`. Hai să ne uităm la un exemplu:

```dart
int prim(int numar) {
  for(int d = 2; d < numar / 2; d++){
    if(numar % d == 0){
      return false;
    }
  }
  return true;
}

void main(){
  print("13 este un numar prim? ${prim(13)}"); // Prints: 13 este un numar prim? true
}
```

Cu toate acestea, există niște mari diferențe. În Dart, funcțiile pot lua parametri după nume. De exemplu, o funcție definită în felul acesta:

```dart
void foo(int a, {int? b, int? c}) {
  return;
}
```

Se va apela in felul acesta:

```dart
void main() {
  foo(1, b: 2, c: 3);
}
```
![confused](img/confused.jpg)

Dacă înconjurăm niște parametri în acolade în antetul funcției, acei parametri devin opționali și trebuie numiți atunci când sunt pasați la apel.

Tipul unui parametru opțional trebuie să aibă `?` la final, cum ar fi `int?`. Dacă acel parametru nu este pasat, atunci în cadrul funcției parametrul va fi `null`.

```dart
void foo(int a, {int? b, int? c}) {
  print(b);
}

void main(){
  foo(1); // Prints: null.
  foo(1, b: 2) // Prints: 2.
}
```

Dacă totuși vrei să fie un parametru numit și să nu fie optional (sau cum se referă în documentația oficială: "nullable"), putem să folosim cuvântul cheie "required" când declarăm parametrul din funcție. În felul acesta, Dart ne va avertiza înainte să rulăm că trebuie să dăm o valoare parametrilor "b" și "c".

```dart
void foo(int a, {required int b, required int c}) {
  print(b);
}
```

Conceptul de "nullable" este mai avansat și nu are rost să ne legăm de el aici. Ideea este că poți să declari o variabilă "nullable" în afara antetului unei funcții, iar acea variabilă fie va fi de tipul declarat, fie null. Te ajută să știi exact dacă ai o informație în acea variabilă sau nu.

```dart
void main() {
  int? a;
  print(a); // Prints: null
  a = 2;
  print(a); // Prints: 2.
}
```

## Funcții ca variabile

![what](https://media.tenor.com/tqERWt8lBYEAAAAC/calculating-puzzled.gif)

Ok, let me explain:

În Dart, funcțiile pot fi declarate în mod static așa cum sunt în C/C++, dar pot fi declarate și dinamice. Funcțiile dinamice sunt declarate pe loc direct în codul nostru. Aceste funcții dinamice pot fi atribuite unei variabile, iar acea variabilă va avea tipul `Function`. După aceea, aceste variabile pot fi apelate ca funcții folosind metoda `.call()`.

```dart
void main() {
  var doSomething = () {
    print('Something');
  }

  doSomething.call();
}
```

În acest exemplu, am declarat o funcție dinamică și am atribuit-o variabilei `doSomething`. Observăm că pentru a crea o funcție dinamică este ca și cum am scoate tipul de întoarcere și numele unei funcții normale și ne rămân doar parametrii să-i definim. În cazul de sus, nu avem parametrii, dar funcțiile dinamice pot avea parametrii la fel ca cele statice.

```dart
void main() {
  var doSomething = (String something) {
    print(something);
  }

  doSomething.call("Something");
}
```

Observați cum atunci când funcția dinamică primește parametrii, aceștia apar ca și parametrii metodei `.call()`.

Acest concept este de ajutor atunci când vrem să specificăm un anumit comportament când un eveniment are loc într-o aplicație. De exemplu, vom lucra cu butoane și dorim ca acel buton să facă ceva atunci când este apăsat. Atunci am defini butonul în felul următor:

```dart
ElevatedButton(
  child: Text('Press me'),
  onPressed: () {
    print('YAHHOO!!');
  }
)
```

> [Deschide editorul: ](https://dartpad.dev/?id=3594da47b00c383e29b94b716ffd956e)

Observați că și atunci când creați widget-uri, modul în care specificați atributele unui widget este similar cu modul în care pasați parametrii către o funcție.

## Exerciții:

### Clasicul foo bar:

> [Deschide editorul: ](https://dartpad.dev/?id=8ea350377714efcd8efd8bdf7c1ecf56)

### Numero Numero

> [Deschide editorul: ](https://dartpad.dev/?id=cb2eb48afc71152cb79e350389c654cf)