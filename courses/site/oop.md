# Programarea Orientata pe Obiect

Ok, let's take it from the start.

### Rădăcinile POO/OOP

Care este primul programator orientat pe obiecte?

![plato](https://www.worldhistory.org/img/r/p/750x750/12427.jpg?v=1686077046)

Băiatul ăsta din Atena care a trăit acum 2500 de ani a fost primul care s-a gândit la programarea orientată pe obiect. Doar că nu o știa.

Cum a reușit? Care e secretul succesului său? Este oare barba? (nu)

Platon a observat un adevăr foarte elementar:

El a văzut multe pisici pe străzile Atenei, dar a observat că deși noi putem foarte ușor să recunoaștem ce e aia o pisică, toate pisicile sunt relativ diferite.

A observat că există pisici negre, albe, maronii. A observat că unele au blană multă, altele deloc. Așa că a teoretizat despre o lume care există dincolo de orizonturile înțelegerii, o sferă superioară a ideilor, și undeva în acea sferă există o **Pisică Cosmică Chintesențială** din care derivă toate celelalte pisici.

Și în sfera noastră există doar instanțe ale acestei pisici cosmice care sunt imperfecte și conțin diferite particularități cum sunt cele listate mai sus.

Platon și-a petrecut mult din viață încercând să vadă cum ar putea arăta aceste **ființe cosmice chintesențiale** prin a încerca să găsească lucruri comune între diferite ființe.

Desigur este simplu să ne dăm seama că Platon a greșit în totalitate cu teoriile sale, dar a observat o idee de bază care mai târziu a fost dezvoltată de un alt barbos vreo 2000 de ani mai târziu.

![darwin](https://th-thumbnailer.cdn-si-edu.com/rwl5lK6jbJXAOlnr603C2ioHfC4=/1072x720/filters:no_upscale()/https://tf-cmsv2-smithsonianmag-media.s3.amazonaws.com/filer/Charles-Darwin-1880-631.jpg)

Băiatul ăsta a dus teoria mai departe. A spus: multe pisici au caracteristici similare între ele, dar au caracteristici similare și cu alte feline. De ce?

Păi, istoria ne-a arătat că de fapt Darwin contempla la bazele teoriei evoluției.

Mulți nu înțeleg această teorie a evoluției și o rezumă la:

> 'Oamenii se trag din maimuțe'

Dar în realitate, oamenii nu se trag din maimuțe, ci de fapt oamenii și maimuțele se trag dintr-un strămoș comun care posedă câteva din calitățile care se regăsesc atât în oameni cât și în maimuțe, din care au evoluat atât oamenii cât și restul primatelor.

![evolution](https://anthrospin.files.wordpress.com/2019/01/phylogeny.jpg?w=1040)


Ideea aici este că atât noi cât și maimuțele am **moștenit** diferite particularități de la o ființă care exista înainte. Aceste particularități sunt grupate în diferite grupuri abstracte cum este: primata, mamifer, pasăre, pește etc...

Deci putem să spunem lucruri cum ar fi: omul este o primată. Toate primatele fac pui vii, deci toate primatele sunt mamifere, deci toți oamenii sunt mamifere. Și tot așa.

### No, și ce? De ce îmi spui toate astea?

Ideea este că programarea orientată pe obiect se bazează pe relații de moștenire între diferite clase de obiecte.

Putem să spunem că pisica abstractă a lui Platon, este de fapt un set de atribute și comportamente care descriu ce înseamnă o pisică, numit de acum **clasa pisică** și putem spune că pisicile din Atena sunt instanțe ale acestei clase, numite de acum **obiectul pisică**.

Putem și să spunem că multe dintre aceste atribute le-a luat de la un strămoș felin, adică le-a moștenit.

Noi, putem să introducem o astfel de structură și în codul nostru, folosind clase și obiecte.

Haideți să definim împreună clasa pisică:

<!-- Add the finished code for those who were not present -->
<!-- color, weight, wiskerLength -->
```dart
class Cat {
  String color;
  double weight;
  double tailLength;
  double wiskerLength;
}
```

Iată textul cu diacriticele adăugate:

Ideea este că această clasă este degeaba, dacă nu o putem folosi, așa că haideți să creem un obiect din clasa pisică, dându-i câteva atribute de la noi.

Ca să putem să creăm un obiect din clasa `Cat` avem nevoie ca clasa noastră să definească o funcție specială numită `constructor`. Constructorul este o funcție care nu întoarce nimic și al cărui nume este exact același cu numele clasei. Observăm că în header-ul constructorului, avem definite atributele pe care dorim să le inițializăm:

```dart
class Cat {
  String color;
  double weight;
  bool hasHeterochromia;
  double wiskerLength;

  Cat(
    this.color,
    this.weight,
    this.hasHeterochromia,
    this.wiskerLength,
  );

}
```

Odată ce avem constructorul nostru, noi putem să-l folosim ca să creăm un obiect de tip pisică, sau altfel spus: O instanță a clasei pisică.

```dart
void main(){
  Cat miți = Cat(
    "red",
    15,
    true,
    10,
  );

  print(miți.weight); // prints 15

  miți.weight = 20; // Getting chonkier by the MINUTE!

  print(miți.weight); // prints 20
}
```

> 💡 Observăm cum putem să accesăm atributele unui obiect prin sintaxa: obiect.atribut

Bun, dar pisica noastră nu prea face nimic, haideți să definim și un comportament pe pisica noastră, și anume să creăm câteva funcții care descriu un comportament normal al unei pisici:

<!-- purr, speak, break(Vase) -->
```dart
class Cat {
  String color;
  double weight;
  bool hasHeterochromia;
  double wiskerLength;

  Cat(
    this.color,
    this.weight,
    this.hasHeterochromia,
    this.wiskerLength,
  );

  void speak() {
    print('miau!');
  }

  void breakVase(Vase vase){
    vase.isBroken = true;
  }

}
```

Unde `Vase` este o altă clasă, să spunem că conține doar două atribute:

<!-- color, isBroken -->
```dart
class Vase {
  bool isBroken = false;
}
```

Observăm că noi putem să trimitem o clasă ca un argument la o funcție. În acest caz, poate dorim să implementăm un joc în care pisicile sparg vaze în funcție de cum apăsăm pe butoane.

> 💡 Ce este interesant aici este că noi putem să oferim valori de bază anumitor atribute. Deoarece am specificat că default-ul la isBroken este fals, nu mai trebuie să definim un constructor care să primească o valoare pentru acel atribut.

```dart
void main() {
  Cat miți = Cat(
    "red",
    15,
    true,
    10,
  );

  Vase vase = Vase();

  print(vase.isBroken); // Prints: false
  miți.breakVase(vase);

  print(vase.isBroken); // Prints: true
}
```

Bun, dar care este treaba cu moștenirea? Păi, să spunem că dorim să mai definim o clasă de cățel. Să spunem că arată așa:

<!-- color, weight, snoutLength, speak -->
```dart
class Dog {
  String color;
  double weight;
  double snoutLength; // lungimea botului.

  Dog(
    this.color,
    this.weight,
    this.snoutLength,
  );

  void speak() {
    print('ham!');
  }
}
```

Observăm că sunt multe proprietăți pe care le au atât pisica, cât și cățelul. Așa că, folosind moștenirea, ne putem simplifica codul în felul următor. Putem defini o clasă abstractă numită `Mamifer` care are toate proprietățile pe care le au câinii și pisicile în comun:

<!-- create abstract class -->
```dart
abstract class Mamifer {
  String color;
  double weight;

  Mamifer(
    this.color,
    this.weight,
  );
}
```
Faptul că această clasă este marcată ca `abstract` înseamnă că această clasă nu poate fi folosită pentru a produce un obiect niciodată. Nu exista defapt obiecte de tip mamifer în lumea reală, ci doar exemple de mamifer. Clase care moștenesc mamifer. Această clasă poate doar să fie moștenită de alte clase în următorul mod:

```dart
class Cat extends Mamifer {
  bool hasHeterochromia;
  double wiskerLength;

  Cat(
    super.color,
    super.weight,
    this.hasHeterochromia,
    this.wiskerLength,
  );

  void speak() {
    print('miau!');
  }
}

class Dog extends Mamifer{
  double snoutLength;

  Dog(
    super.color,
    super.weight,
    this.snoutLength,
  );

  void speak() {
    print('ham!');
  }
}
```

În acest fel, putem să izolăm proprietățile care sunt comune tuturor mamiferelor, iar în clasele `Cat` și `Dog` să ne concentrăm doar pe ceea ce face cațeii și pisicile să fie diferiți.

Ce este important de reținut este că și clasele abstracte au un constructor (deși nu este folosit), iar dacă vrem să inițializăm acele atribute care aparțin de clasa din care se moștenește, în loc să folosim `this.color`, folosim `super.color`, deoarece `color` aparține acum de `super`-ul lui `Cat`.

### Metode abstracte și Polimorfism

Noi totuși observăm că am putea să mutăm și funcția `speak` în clasa `Mamifer`, deoarece atât câinele, cât și pisica vorbesc. Problema este că atunci când pisica vorbește, ea face "miau". Câinele face "ham". Ce ne facem noi?

Ideea este că, deși fiecare clasă are o implementare a funcției `speak`, noi putem să mutăm funcția `speak` în clasa `Mamifer`, dar fără să specificăm exact ce să facă. Prin asta, noi forțăm toate clasele care moștenesc `Mamifer` să implementeze funcția `speak` în felul lor separat.

```dart
abstract class Mamifer {
  String color;
  double weight;

  Mamifer(
    this.color,
    this.weight,
  );
  // Cand nu specificam un corp al functiei, punem doar ;
  void speak();
}
```

Dacă facem acest lucru, în editorul nostru s-ar putea să observăm că orice clasă care moștenește `Mamifer` dă eroare dacă nu implementăm funcția `speak`. Hai să spunem că definim clasa `Fox` care moștenește `Mamifer`:

```dart
class Fox extends Mamifer {

  Fox(
    super.color,
    super.weight,
  );

  @override
  void speak() {
    // WHAT DOES THE FOX SAY???
    print('...???');
  }
}
```

Când implementăm o metodă, în general, o marcam cu acel `@override`. Este opțional, dar ne ajută să știm că metoda aceasta nu este definită de fapt în clasa curentă, ci în cea superioară. Trebuie să implementăm această metodă în toate clasele care moștenesc `Mamifer`.

Ok, ok. Dar, fiți pe fază:

```dart
void main() {
  Mamifer a = Cat("Red", 10, true, 15);
  Mamifer b = Dog("Blue", 10, 15);

  a.speak();
  b.speak();
  print(a.color);
  print(b.snoutLength);
}
```
Ce se întâmplă aici?

Observăm că noi putem să definim o variabilă să fie de tip `Mamifer`, dar să o inițializăm cu constructorul unei clase moștenitoare. Când rulăm fiecare instrucțiune din `main`, observăm că:

- `a` va afișa "miau"
- `b` va afișa "ham"

Deși amândouă sunt definite ca mamifere, instanțele specifice sunt `Cat` și `Dog`.

- `a.color` va printa "Blue"
- `b.snoutLength` va da o eroare

De ce?

Pentru că, deși obiectele sunt clase diferite, dacă sunt stocate într-o variabilă de tip `Mamifer`, noi vom avea acces doar la proprietățile care sunt definite pentru toate mamiferele.

Bine, și cu ce mă ajută? Hai să spunem că avem o clasă `PetClinic` care să reprezinte un pet store și să o instantiem:

```dart
class PetClinic {
  List<Mamifer> animals;

  PetClinic(this.animals);
}

void main() {
  var petClinic = PetClinic(
    [
      Cat("Red", 10, true, 15),
      Fox(),
      Dog("Yellow", 20, 15),
      Cat("Black", 10, false, 15),
    ],
  );
}
```

Deci tocmai am definit o clinică de animale de companie care are o listă de animale pe care le are în grijă. Aceste animale pot să fie de orice tip, dar din perspectiva clinicii, ele sunt toate mamifere care trebuie îngrijite similar. Să spunem că această clinică ar avea o metodă de `singTogether()` care face toate animalele din clinică să vorbească:

```dart
class PetClinic {
  List<Mamifer> animals;

  PetClinic(this.animals);

  void singTogheter() {
    for(Mamifer pet in animals) {
      pet.speak();
    }
  }
}
```
Această calitate a OOP-ului se numește polimorfism. Adică o clasă abstractă poate să ia mai multe forme și să se comporte în mod diferit, în funcție de ce fel de obiect este (Cat, Dog sau Fox). Și este de fapt unul dintre conceptele de bază pe care este construit Flutter.

### Parametrii denumiți (extra)

La fel cum putem să avem funcții cu parametri opționali și denumiți, la fel putem să avem parametri opționali și denumiți și în constructorul unei clase. De exemplu, mai sus am creat mai multe mamifere în felul următor:

```dart
Mamifer a = Cat("Red", 10, true, 15);
Mamifer b = Dog("Blue", 10, 15);
```

Este fain și este ok momentan, dar vor exista multe clase în codul nostru de Flutter care vor avea multe atribute. Dacă ajungem la 10 atribute, deja devine foarte greu să ținem evidența ordinii lor, așa că în general este preferat să declarăm constructorii cu parametri opționali. Deoarece avem nevoie de toate atributele pisicii, acestea vor fi `required`:

```dart
class Dog extends Mamifer{
  double snoutLength;

  Dog({
    required super.color,
    required super.weight,
    required this.snoutLength,
  });

  void speak() {
    print('ham!');
  }
}
```

Avantajul de a scrie constructorii cu parametri numiți este faptul că nu mai trebuie să le ținem minte ordinea și codul devine mult mai lizibil:

```dart
void main() {
  Dog cuțu = Dog(
    color: "red",
    weight: 19,
    snoutLength: 10,
  );
}
```

### De la căței și pisici la widget-uri și aplicații

Partea cea mai faină este că noi putem să aplicăm modul acesta de gândire în multe cazuri, în funcție de nevoile programului pe care dorim să-l scriem. Dacă facem un joc în care pisicile se plimbă pe hartă și sparg vaze, poate acea funcție de break vase este un comportament relevant, însă dacă vrem să facem o aplicație în care ne creștem pisica, poate am vrea proprietăți cum ar fi mâncare, sănătate, curățenie etc.

Putem nici să nu vorbim despre pisici. Putem să modelăm lucruri abstracte după ideile astea, cum ar fi: ✨ ***Widgets!*** ✨

Dacă stai să te gândești, și widget-urile sunt niște clase abstracte care au un comportament comun, și anume toate trebuie să randeze `ceva?` pe ecran, folosind funcția `build`.

Ei bine, la fel cum toate animalele scot un sunet, la fel și toate widget-urile construiesc elemente în interfață prin funcția `build`. În această funcție, noi putem să descriem felul în care widget-ul ar trebui să arate, prin a folosi alte widget-uri.

Această funcție `Widget build(BuildContext context)` este moștenită de la părintele `StatelessWidget`, în felul următor:

<!-- Introdu cum se delcara un widget -->
```dart
class YellowSquare extends StatelessWidget {

  Widget build(BuildContext context) {
    return Container(
      width: 10,
      height: 10,
      color: Colors.yellow,
    );
  }
}
```


Deja am mai fost pe aici în cursul trecut prin exemple. Observăm că avem clasa noastră de widget, care moștenește `StatelessWidget` și implementează funcția `build`.

Ei bine, când Flutter se uită la clasa pe care tocmai ai construit-o, el nu trebuie să știe că e un `YellowSquare` ca să îl construiască. El are nevoie strict de funcția `build` care îi spune exact cum trebuie să arate acel pătrat galben.

Anyway. Dacă ai ajuns până aici, meriți niște poze cu animăluțe! 🐱🐶📷

![miti](https://images.ctfassets.net/ub3bwfd53mwy/5zi8myLobtihb1cWl3tj8L/45a40e66765f26beddf7eeee29f74723/6_Image.jpg?w=750)
![cutu](https://images.unsplash.com/photo-1615751072497-5f5169febe17?auto=format&fit=crop&q=80&w=1000&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8Mnx8Y3V0ZSUyMGRvZ3xlbnwwfHwwfHx8MA%3D%3D)
![cutu](https://i.pinimg.com/736x/45/75/a6/4575a68f26e1c9fc0d69945b0d261e3a.jpg)



<!-- How to improve this course? 
  - Set up the terms: clasa superioara, clasa mostenitoare, clasa abstracta.
  - Fa metafora mai buna
    - concentreaza-te pe plato, si dupa pe darwin. Mostenirea ar trebui sa vina ca o nevoie, nu ca un fapt deja dat.
  - Niste poze cu pisici. Actually... MULTE POZE CU PISICI!!!!
  - maybe spend more time on constructors. Do the body constructor first.
 -->