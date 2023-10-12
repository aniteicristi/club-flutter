# Programarea Orientata pe Obiect

Ok, let's take it from the start.

### Rădăcinile POO/OOP

Care este primul programator orientat pe obiecte?

![plato](https://www.worldhistory.org/img/r/p/750x750/12427.jpg?v=1686077046)

Baiatul asta din atena care a trait acum 2500 de ani a fost primul care s-a gandit la programarea orientata pe obiect. Doar ca nu o stia.

Cum a reusit? Care e secretul succesului sau? Este oare barba? (nu)

Plato a observat un adevar foarte elementar:

El a vazut multe pisici pe strazile Atenei, dar a observat ca desi noi putem foarte usor sa recunoastem ce e aia o pisica, toate pisicile sunt relativ diferite.

A observat ca exista pisici negre, albe, maronii. A observat ca unele au blana multa, altele deloc. Asa ca a teoretizat despre o lume care exista dincolo de orizonturile intelegerii, o sfera superioara a ideilor, si undeva in acea sfera exista o **Pisica Cosmica Abstracta** din care deriva toate celelalte pisici.

Si in sfera noastra exista doar instante ale acestei pisici cosmice care sunt imperfecte si contin diferite particularitati cum sunt cele listate mai sus.

Platon si-a petrecut mult din viata incercand sa vada cum ar putea arata aceste **fiinte cosmice abstracte** prin a incerca sa gaseasca lucruri comune intre diferite fiinte. Acesta a fost un proces haios, mai ales cand a interactionat cu maritul Diogene.

Desigur este simplu sa ne dam seama ca Plato a gresit in totalitate cu teoriile sale, dar a observat o idee de baza care mai tarziu a fost dezvoltata de un alt barbos vreo 2000 de ani mai tarziu:

![darwin](https://th-thumbnailer.cdn-si-edu.com/rwl5lK6jbJXAOlnr603C2ioHfC4=/1072x720/filters:no_upscale()/https://tf-cmsv2-smithsonianmag-media.s3.amazonaws.com/filer/Charles-Darwin-1880-631.jpg)

Baiatul asta a dus teoria mai departe. A spus: multe pisici au caracteristici similare intre ele, dar au caracteristici similare si cu alte feline. De ce?

Pai, istoria ne-a aratat ca defapt Darwin contempla la bazele teoriei evolutiei. 

Multi nu inteleg aceasta teorie a evolutiei si o rezuma la:

> "Oamenii se trag din maimute"

Dar in realitate, oamenii nu se trag din maimute, ci defapt oamenii si maimutele se trag dintr-un stramos comun care poseda toate calitatile care se regasesc atat in oameni cat si in maimute, din care au evoluat atat oamenii cat si restul primatelor.

![evolution](https://anthrospin.files.wordpress.com/2019/01/phylogeny.jpg?w=1040)

Ideea aici este ca atat noi cat si maimutele am **mostenit** diferite particularitati de la o fiinta care exista inainte. Aceste particularitati sunt grupate in diferite grupuri abstracte cum este: primata, mamifer, pasare, peste etc...

Deci putem sa spunem lucruri cum ar fi: omul este o primata. Toate primatele fac pui vi, deci toate primatele sunt mamifere, deci toti oamenii sunt mamifere.

### No, și ce? De ce imi spui toate astea?

Ideea este ca programarea orientata pe obiect se bazeaza pe relatii de mostenire intre diferite clase de obiecte.

Putem sa spunem ca pisica abstracta a lui Platon, este defapt un set de atribute si comportamente care descriu ce inseamna o pisica, numit de acum **clasa pisica** si putem spune ca pisicile din Atena sunt instante ale acestei clase, numite de acum **obiectul pisica**.

Putem si sa spunem ca multe dintre aceste atribute le-a luat de la un stramos felin, adica le-a mostenit.

Noi, putem sa introducem o astfel de structura si in codul nostru, folosind clase si obiecte.

Haideti sa definim impreuna clasa pisica:

<!-- Add the finished code for those who were not present -->
<!-- color, weight, wiskerLength -->

Ideea este ca aceasta clasa este degeaba, daca nu o putem folosi, asa ca haideti sa creem un obiect din clasa pisica, dandu-i cateva atribute de la noi.

Bun, dar pisica noastra nu prea face nimic, haideti sa definim si un comportament pe pisica noastra, si anume sa creem cateva functii care descriu un comportament normal al unei pisici:

<!-- purr, speak, break(Vase) -->

Unde vase este o alta clasa care sa spunem ca contine doar 2 atribute:

<!-- color, isBroken -->


Bun, dar care e treaba cu mostenirea? Pai, sa spunem ca dorim sa mai definim o clasa de catel. Sa spunem ca arata asa:

<!-- color, weight, snoutLength, speak -->

Observam sunt multe proprietati pe care le au si pisica si catelul. Asa ca folosind mostenirea, ne putem simplifica codul in felul urmator:

<!-- create abstract class -->


### De la catei si pisici la widgeturi si aplicatii

Partea cea mai faina este ca noi putem sa aplicam modul asta de gandire in multe cazuri, in functie de nevoile programului pe care dorim sa il scriem. Daca facem un joc unde pisicile se plimba pe harta si sparg vaze, poate acea functie de break vase este un comportament relevant, insa daca vrem sa facem o aplicatie in care ne crestem pisica, poate am vrea proprietati cum ar fi mancare, sanatate, curatenie etc.

Putem nici sa nu vorbim despre pisici. Putem sa modelam lucruri abstracte dupa ideeile astea, cum ar fi: ✨ ***Widgets!*** ✨

Daca stai sa te gandesti, si widgeturile sunt niste clase abstracte care au un comportament comun, si anume toate trebuie sa randeze `ceva?` pe ecran, folosind functia build.