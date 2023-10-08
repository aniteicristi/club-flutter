# Căței pe mobil

În acest exercițiu, vom vedea cum putem insera imagini în aplicația noastră.

Imaginile sunt create cu widget-ul `Image()`. Acest widget are 3 constructori (sau forme) în funcție de sursa imaginii:

- `Image.asset()` va afișa o imagine din lista de resurse (assets). Un asset este un fișier care este încărcat în memoria RAM odată cu întreaga aplicație și este specificat într-un mod aparte (vom vedea mai târziu).
- `Image.memory()` va afișa o imagine din memoria telefonului. Este util atunci când doriți să selectați o imagine de pe telefon și să o previzualizați în aplicație.
- `Image.network()` va afișa o imagine de pe internet, care va fi descărcată de la link-ul specificat ca prim parametru.

Noi ne vom uita la `Image.network()` în acest exercițiu.

Ca întotdeauna, rezolvați //TODO-urile din cod și faceți modificările conform instrucțiunilor.

Dacă vă blocați, puteți să întrebați colegii. Vom aborda acest exercițiu la ședința de data viitoare dacă există confuzii.

> [Deschide editorul: ](https://dartpad.dev/?id=f78c4281bf5e1ba3f04c7ddc9973be3b)