# Text Urât și Containere Urâte

Flutter e creeat in principal pentru realizarea de interfete. De aceea, multe dintre widget-urile noastre expun modalitati de a le stiliza. Astazi ne vom uita pe texte si pe containere.

Pentru a incepe, haide-ti sa ne clonam proiectul. Selectati folderul cu proiectele voastre si deschideti cmd (puteti tasta cmd in bara de sus).

Odata in cmd, copiati si paste-uiti urmatoarea comanda:

```bash
git clone https://github.com/club-flutter-blaga/ugly_text.git
```

La finalul executiei, in folderul cu proiecte ar trebui sa aveti un folder numit simple_login. Deschideti acel folder in visual studio code.

?> 💡 Daca aveti erori, trebuie sa va rulati comanda `flutter pub get`, ca sa va instalati dependintele.

Odata ce aveti instalat totul, puteti sa rulati proiectul, ori din terminal cu `flutter run` ori din vs code din a patra iconiță din stanga.

# Task

La final, cele doua pagini din aplicatia de pe github trebuie sa arate asa:

![uglyText](../img/texte.png)

Primul text este mare, cu fontSize 32

Al doilea text e gri, cu un font size de 22

Al treilea text e italic

Al patrulea text este cu textAlign: TextAlign.justify

Al cincilea text foloseste fontul "Dancing Script" (puteti sa folositi ce vreti)

![uglyText](../img/containere.png)


Primul container e albastru si are un borderRadius de `BorderRadius.all(30)`

Al doilea e galben si are un borderRadius de `BorderRadius.all(180)`

Al treilea este rosu, si are un Border.all(width: 10, color: Colors.purple).