# Programarea Orientata pe Obiect

Ok, let's take it from the start.

### Rădăcinile POO/OOP

Care este primul programator orientat pe obiecte?

![plato](https://www.worldhistory.org/img/r/p/750x750/12427.jpg?v=1686077046)

Baiatul asta din atena care a trait acum 2500 de ani a fost primul care s-a gandit la programarea orientata pe obiect. Doar ca nu o stia.

Cum a reusit? Care e secretul succesului sau? Este oare barba? (nu)

Plato a observat un adevar foarte elementar:

El a vazut multe pisici pe strazile Atenei, dar a observat ca desi noi putem foarte usor sa recunoastem ce e aia o pisica, toate pisicile sunt relativ diferite.

A observat ca exista pisici negre, albe, maronii. A observat ca unele au blana multa, altele deloc. Asa ca a teoretizat despre o lume care exista dincolo de orizonturile intelegerii, o sfera superioara a ideilor, si undeva in acea sfera exista o **Pisica Cosmica Chintesentiala** din care deriva toate celelalte pisici.

Si in sfera noastra exista doar instante ale acestei pisici cosmice care sunt imperfecte si contin diferite particularitati cum sunt cele listate mai sus.

Platon si-a petrecut mult din viata incercand sa vada cum ar putea arata aceste **fiinte cosmice chintesentiale** prin a incerca sa gaseasca lucruri comune intre diferite fiinte.

Desigur este simplu sa ne dam seama ca Plato a gresit in totalitate cu teoriile sale, dar a observat o idee de baza care mai tarziu a fost dezvoltata de un alt barbos vreo 2000 de ani mai tarziu:

![darwin](https://th-thumbnailer.cdn-si-edu.com/rwl5lK6jbJXAOlnr603C2ioHfC4=/1072x720/filters:no_upscale()/https://tf-cmsv2-smithsonianmag-media.s3.amazonaws.com/filer/Charles-Darwin-1880-631.jpg)

Baiatul asta a dus teoria mai departe. A spus: multe pisici au caracteristici similare intre ele, dar au caracteristici similare si cu alte feline. De ce?

Pai, istoria ne-a aratat ca defapt Darwin contempla la bazele teoriei evolutiei. 

Multi nu inteleg aceasta teorie a evolutiei si o rezuma la:

> "Oamenii se trag din maimute"

Dar in realitate, oamenii nu se trag din maimute, ci defapt oamenii si maimutele se trag dintr-un stramos comun care poseda cateva din calitatile care se regasesc atat in oameni cat si in maimute, din care au evoluat atat oamenii cat si restul primatelor.

![evolution](https://anthrospin.files.wordpress.com/2019/01/phylogeny.jpg?w=1040)

Ideea aici este ca atat noi cat si maimutele am **mostenit** diferite particularitati de la o fiinta care exista inainte. Aceste particularitati sunt grupate in diferite grupuri abstracte cum este: primata, mamifer, pasare, peste etc...

Deci putem sa spunem lucruri cum ar fi: omul este o primata. Toate primatele fac pui vi, deci toate primatele sunt mamifere, deci toti oamenii sunt mamifere. Si tot asa

### No, și ce? De ce imi spui toate astea?

Ideea este ca programarea orientata pe obiect se bazeaza pe relatii de mostenire intre diferite clase de obiecte.

Putem sa spunem ca pisica abstracta a lui Platon, este defapt un set de atribute si comportamente care descriu ce inseamna o pisica, numit de acum **clasa pisica** si putem spune ca pisicile din Atena sunt instante ale acestei clase, numite de acum **obiectul pisica**.

Putem si sa spunem ca multe dintre aceste atribute le-a luat de la un stramos felin, adica le-a mostenit.

Noi, putem sa introducem o astfel de structura si in codul nostru, folosind clase si obiecte.

Haideti sa definim impreuna clasa pisica:

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

Ideea este ca aceasta clasa este degeaba, daca nu o putem folosi, asa ca haideti sa creem un obiect din clasa pisica, dandu-i cateva atribute de la noi.

Ca sa putem sa creem un obiect din clasa `Cat` avem nevoie ca clasa noastra sa defineasca o functie speciala numita `constructor`. Constructorul e o functie care nu intoarce nimic si al carui nume este exact acelasi cu numele clasei.

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

Odata ce avem constructorul nostru, noi putem sa il folosim ca sa creem un obiect de tip pisica, sau altfel spus: *O instanta a clasei pisica*

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

> 💡 Observam cum putem sa accesam atributele unui obiect prin sintaxa: obiect.atribut

Bun, dar pisica noastra nu prea face nimic, haideti sa definim si un comportament pe pisica noastra, si anume sa creem cateva functii care descriu un comportament normal al unei pisici:

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
Unde vase este o alta clasa care sa spunem ca contine doar 2 atribute:

<!-- color, isBroken -->
```dart
class Vase {
  bool isBroken = false;
}
```

Observam ca noi putem sa trimitem o clasa ca un argument la o functie. In acest caz, poate dorim sa implementam un joc unde pisicile sparg vaze in functie de cum apasam pe butoane.

> 💡 Ce e interesant aici este ca noi putem sa oferim valori de baza anumitor atribute. Deoarece am specificat ca default-ul la isBroken e fals, nu mai trebuie sa definim un constructor care sa primeasca o valoare pentru acel atribut.

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

Bun, dar care e treaba cu mostenirea? Pai, sa spunem ca dorim sa mai definim o clasa de catel. Sa spunem ca arata asa:

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

Observam sunt multe proprietati pe care le au si pisica si catelul. Asa ca folosind mostenirea, ne putem simplifica codul in felul urmator. Putem defini o clasa abstracta numita `Mamifer` care are toate proprietatile pe care le au cainii si pisicile in comun:

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
Faptul ca aceasta clasa este marcata ca `abstract` inseamna ca aceasta clasa nu poate fi folosita pentru a produce un obiect niciodata. Aceasta poate doar sa fie mostenita de alte clase in urmatorul mod:

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

In acest fel, putem sa izolam proprietatile care sunt comune tuturor mamiferelor, si in clasa `Cat` si `Dog` sa ne concentram doar pe ce face cainii si pisicile sa fie diferiti.

Ce este important de retinut este ca si clasele abstracte au un constructor (desi nu este folosit), iar daca vrem sa initializam acele atribute care apartin de clasa din care se mosteneste, in loc sa folosim `this.color` folosim `super.color`, deoarece color apartine acum de `super`-ul lui Cat.


### Metode abstracte și Polimorfism

Noi totusi observam ca am putea sa mutam si functia speak in clasa mamifer, deoarece atat si cainele cat si pisica vorbesc. Problema este ca atunci cand pisica vorbeste, ea face maiu. Cainele face ham. Ce ne facem noi?

Ideea este ca desi fiecare clasa are o implementare a functiei speak, noi putem sa mutam functia speak in clasa mamifer, dar fara sa specificam exact ce sa faca. Prin asta, noi fortam toate clasele care mostenesc `Mamifer` sa implementeze functia speak in felul lor separat.

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

Daca facem acest lucru, in editorul nostru s-ar putea sa observam ca orice clasa care mosteneste `Mamifer` da eroare daca nu implementam functia speak. Hai sa spunem ca definim clasa `Fox` care mosteneste mamifer:

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

Cand implementam o metoda, in general o marcam cu acel `@override`. Este optional, dar ne ajuta sa stim ca metoda asta nu e definita defapt in clasa asta, ci in cea superioara.

Ok, ok. Dar. Fiti pe faza:

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
Ce se intampla aici?




Observam ca noi putem sa definim o variabila sa fie de tip mamifer, dar sa o initializam cu constructorul unei clase mostenitoare. Cand rulam fiecare instructiune din main, observam ca:

- a va afisa "miau"
- b va afisa "ham"

Desi amandoua sunt definite ca mamifere, instantele specifice sunt Cat si Dog.

- a.color va printa "Blue"
- b.snoutLength va da o eroare

Ok... De ce?

Pentru ca desi obiectele sunt clase diferite, daca sunt stocate intr-o variabila de tip `Mamifer`, noi vom avea acces doar la proprietatile care sunt definite pentru toate mamiferele.

Bine, si cu ce ma ajuta? Hai sa spunem ca avem o clasa `PetClinic` care sa reprezinte un pet store si sa o instantiem:

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

Deci tocmai am definit o clinica de animale de companie care are o lista de animale pe care le are in grija. Aceste animale pot sa fie de orice tip, dar din perspectiva clinici, ele sunt toate mamifere care trebuie ingrijite similar. Sa spunem ca clinica ar avea o metoda de `singTogheter()` care face toate animalele din clinica sa vorbeasca:


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

Aceasta calitate a OOP-ului se numeste polimorfism. Adica o clasa abstracta poate sa ia mai multe forme si sa se comporte intr-un mod diferit, in functie de ce fel de obiect este (Cat, Dog sau Fox). Si este defapt unul dintre conceptele de baza pe care este construit Flutter.

### Parametrii denumiti (extra)

La fel cum putem sa avem functii cu parametrii obtionali si denumiti, la fel putem sa avem parametrii optionali si denumiti si in constructorul unei clase. De exemplu mai sus am creeat mai multe mamifere in felul urmator:

```dart
Mamifer a = Cat("Red", 10, true, 15);
Mamifer b = Dog("Blue", 10, 15);
```

E fain si e ok momentan, dar vor exista multe clase in codul nostru de flutter care vor avea multe atribute. Daca ajungem la 10 atribute, deja devine foarte greu sa tinem evidenta ordinii lor, asa ca in general e preferat sa declaram constructorii cu parametrii optionali. Deoarece avem nevoie de toate atributele psicii, acestea vor fi `required`:

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

Avantajul de a scrie constructorii cu parametri numiti este faptul ca nu mai trebuie sa le tinem minte ordinea si codul devine mult mai lizibil:

```dart
void main() {
  Dog cuțu = Dog(
    color: "red",
    weight: 19,
    snoutLength: 10,
  );
}
```

### De la catei si pisici la widgeturi si aplicatii

Partea cea mai faina este ca noi putem sa aplicam modul asta de gandire in multe cazuri, in functie de nevoile programului pe care dorim sa il scriem. Daca facem un joc unde pisicile se plimba pe harta si sparg vaze, poate acea functie de break vase este un comportament relevant, insa daca vrem sa facem o aplicatie in care ne crestem pisica, poate am vrea proprietati cum ar fi mancare, sanatate, curatenie etc.

Putem nici sa nu vorbim despre pisici. Putem sa modelam lucruri abstracte dupa ideeile astea, cum ar fi: ✨ ***Widgets!*** ✨

Daca stai sa te gandesti, si widgeturile sunt niste clase abstracte care au un comportament comun, si anume toate trebuie sa randeze `ceva?` pe ecran, folosind functia build.

Ei bine, la fel cum toate animalele scot un sunet, la fel si toate widget-urile construiesc elemente in interfata prin functia `build`. In aceasta functie, noi putem sa descriem felul in care widget-ul ar trebui sa arate, prin a folosi alte widget-uri. 

Aceasta functie `Widget build(BuildContext context)` este moștenita de la parintele `StatelessWidget`, in felul urmator:

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

Deja am mai fost pe aici in cursul trecut prin exemple. Observam ca avem clasa noastra de widget, care mosteneste `StatelessWidget` si implementeaza functia build.

Ei bine, cand flutter se uita la clasa pe care tocmai ai construit-o, el nu trebuie sa stie ca e un `YellowSquare` ca sa il construiasca. El are nevoie strict de functia build care ii spune exact cum trebuie sa arate acel patrat galben.

Anyway. Daca ai ajuns pana aici, meriti niste poze cu animalute! 

![miti](https://images.ctfassets.net/ub3bwfd53mwy/5zi8myLobtihb1cWl3tj8L/45a40e66765f26beddf7eeee29f74723/6_Image.jpg?w=750)
![cutu](https://images.unsplash.com/photo-1615751072497-5f5169febe17?auto=format&fit=crop&q=80&w=1000&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8Mnx8Y3V0ZSUyMGRvZ3xlbnwwfHwwfHx8MA%3D%3D)
![cutu](https://i.pinimg.com/736x/45/75/a6/4575a68f26e1c9fc0d69945b0d261e3a.jpg)



<!-- How to improve this course? 
  - Set up the terms: clasa superioara, clasa mostenitoare, clasa abstracta.
  - Fa metafora mai buna
  - Niste poze cu pisici. Actually... MULTE POZE CU PISICI!!!!
  - maybe spend more time on constructors. Do the body constructor first.
 -->