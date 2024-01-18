# Stiluri

## Text

### General styling

Textul este probabil cel mai simplu widget de stilizat. Pentru a modifica aspectul unui text putem sa modificam. Textul se stilizeaza prin specificarea atributului `style` cu un obiect de tip `TextStyle()`. In acel obiect de text style putem sa specificam urmatoarele:

- **Size** - Putem sa modificam marimea textului (fontului), cu atributul `fontSize`. Acesta reprezinta numarul de pixeli intr-un caracter `m` din fontul acela, ridicat la patrat. 
- **Weight** - Putem sa modificam grosimea textului (fontului), cu atributul `fontWeight`. Putem sa specificam normal sau bold, dar avem mai multe weight-uri din care putem selecta, de la `w100` pana la `w900`, unde `w0` e normal si `w1000` e bold.
- **Style** - Putem sa specificam daca textul e italic sau nu, cu atributul `fontStyle`. Poate sa fie doar normal sau italic.
- **Color** - Putem sa modificam culoarea textului, cu atributul `color`. Acest atribut ia orice culoare din cele existente in obiectul `Colors`.

```dart
Text(
  'Ala bala portocala',
  style: TextStyle(
    fontSize: 15,
    fontWeight: FontWeight.bold,
    fontStyle: FontStyle.italic,
    color: Colors.red,
  ),
)
```

Pentru mai multe proprietati ale `TextStyle()`-ului, accesati aici [https://api.flutter.dev/flutter/painting/TextStyle-class.html](https://api.flutter.dev/flutter/painting/TextStyle-class.html)

### Alinierea textului.

Pe langa aceste stiluri pe care le putem specifica, putem sa modificam si aliniatul textului in pagina. Aliniatele pe care le putem specifica sunt aceleasi ca din word:

- Left
- Right
- Center
- Justify

```dart
Text(
  'Portocale bla bla bla bla bla',
  textAlign: TextAlign.left,
  style: TextStyle(
    color: Colors.red,
  ),
)
```

### Font-uri.

Pentru a specifica un font, putem folosi atributul de pe TextStyle numit `fontFamily`. Fonturile sunt specificate printr-un string, dar trebuie importate in proiectul nostru dintr-un fisier. Acest proces este enervant si incet. Dar avem o alternativa:

Google ofera o librarie mare de font-uri care ne lasa sa le folism direct din flutter fara sa le mai important.

Aceasta librarie se numeste `google_fonts` si trebuie adaugata la dependinte in fisierul pubspec.yaml.

Odata adaugat, putem sa folosim fonturile din libraria lor, disponibile aici:

[https://fonts.google.com/](https://fonts.google.com/)

Tot ce trebuie sa facem pentru a folosi acele font-uri este a atribui la atributul `style` al unui text unul dintre fonturile accesibile de pe obiectul `GoogleFonts`.

```dart
Text(
  'haha',
   style: GoogleFonts.roboto,
)
```
## Containere

Pentru a modifica stilizarea unui container, trebuie sa ii atribuim atributului `decoration` un obiect de tip `BoxDecoration`.

In acel obiect putem sa specificam urmatoarele:

- Culoarea prin atributul `color`, care poate lua orice culoare din `Colors`.
- Cat de rotunde ii sunt colturile, prin atributul `borderRadius`. 
  - Valorile pot fi specificate pentru fiecare colt a containerului, sau pentru toate folosind: `BorderRadius.all(radius)` unde radius este un numar real.
- Putem stiliza bordura containerului daca ii atribuim la `BoxDecoration` in atributul `border` un obiect de tip `Border.all()`.
  - In acel obiect `Border.all()` putem specifica `width`-ul bordurii, dar și culoarea prin `color`.
  - `Border.all` inseamna ca vrem sa specificam acelasi stil pentru fiecare bordura a container-ului. Noi putem sa stilizam fiecare bordura diferit (cea de sus, cea de jos, cea din stanga si cea din dreapta) la fel cum folosim si `EdgeInsets.all()`. Pentru a stiliza fiecare bordura individual, folosim doar `Border()`.


```dart
Container(
  width: 100,
  height: 100,
  decoration: BoxDecoration(
    color: Colors.yellow,
    borderRadius: BorderRadius.all(30),
    border: Border.all(
      width: 30,
      color: Colors.blue,
    )
  )
)
```