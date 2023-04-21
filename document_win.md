# REACT JS

## I. Prerequis: 
Au d�but rien.

## II. Premier code motivant React

### 2.1 Code html/css classique
Nous allons utiliser codepen.io (penser � ouvrir un compte pour pouvoir enregistrer les avancements). J'ai commenc� � cr�er un code html comme dans la partie `html`

```html
<div class="person">
  <H1>Max</H1>
  <p>your age : 42</p>
</div>

<div class="person">
  <H1>Manu</H1>
  <p>your age : 28</p>
</div>
```
et la classe `".person"` est impl�ment�e en `"css"` comme suit:

```css
.person{
  display: inline-block;
  margin: 10px;
  border: 1px solid #ccc;
  box-shadow: 0 2px 2px #ccc;
  width: 200px;
  padding: 20px;
}
```
Sur codepen, je devrais avoir ceci:
![](img/example1_copen.png)


La sortie devrait nous donner ceci:
![](img/result1.png)


### 2.2 Rajout des librairies React.js et ReactDOM
Pour l'instant, aucun code React mais on comprend que les diff�rents tags `<div>`sont toujours structur� de la m�me mani�re et donc on pourrait "eventuellement" automatiser la cr�ation d'un composant `<div>`comme ce que nous avons ci-dessus. En effet, React permet par exemple de cr�er des composants r�utilisables et param�trables.

Essayons de rajouter un petit parfum de `React` alors.
La premi�re chose � faire est d'aller importer la librairie `React.js` en cliquant (dans codepen.io) sur le bouton `settings`.
![](img/button_setting.png).

Et donc dans l'interface qui s'affiche, dans la partie JS, choisir `React`et choisir la derni�re version qui s'affiche.

![](img/copde_react.png)

Et cliquez `save and close`

De la m�me mani�re rajoutez `ReactDOM`

![](img/react-dom.png)

Enfin, comme React, n'utilises pas seulement le javascript classique mais des versions nouvelles, il faut choisir dans la partie `Javascript preprocessor`, la version `Babel` (plus tard, nous le comprendrons)

![](img/js_babel.png)

### 2.3 Creation d'un composant React
Nous allons convertir le `<div>` que nous avions en un composant React. 
Dans la partie `JS` de codepen, commen�ons par cr�er une fonction que nous allons nommer `Person`. Dans cette function, nous allons juste retourner le code complet du `<div>` (la syntaxe de ce code retourn� est appel� `jsx` - https://fr.reactjs.org/docs/introducing-jsx.html - une sorte de m�lange entre du html et du js). Ce JSX ne fonctionnerait pas si nous n'avions pas choisi `Babel` dans les preprocesseurs.

```js
function Person(){
  return (
    // code JSX � ins�rer ici    
  );
}
```

Le code devient alors comme ceci:

```js
function Person(){
  return (
    <div class="person">
      <H1>Max</H1>
      <p>your age : 42</p>
    </div>
  );
}
```
Cr�er la fonction n'est pas suffisante, bien, s�r et il faut maintenant faire le rendu du JSX. Pour cela, il faut utiliser `ReactDOM.render()` (en gros, cela permet de faire le rendu [afficher], une fonction qui retourne un JSX comme un composant, en le sp�cifiant comme un tag html - ici ce sera le tag `<Person />`).

La fonction `render()`, prend deux arguments:
* le premier est l'objet JSX (le tag correspondant au nom de la fonction)
* le deuxi�me est l'endroit o� on veut faire le rendu dans le HTML.

Avant de donner la syntaxe, nous allons d'abord modifier un peu le HTML, pour cr�er un tag `<div id="p1"></div>` qui est vide et qui nou servira � afficher notre JSX.

Le code HTML devient alors comme ceci:

```html
<div id="p1"></div>

<div class="person">
  <H1>Manu</H1>
  <p>your age : 28</p>
</div>
```
Maintenant, nous allons rajouter, dans le JS, le code qui permettra de faire le rendu de la fonction `Person` dans le `<div id="p1">` qui initialement est vide (pas de contenu).

Rajouter dans le code JS
```js
function Person(){
  return (
    <div class="person">
      <H1>Max</H1>
      <p>your age : 42</p>
    </div>
  );
}

// rajouter la fonction render
ReactDOM.render(<Person/>, document.querySelector("#p1"));
```
* `<Person />`: on a dit que le JSX doit �tre sp�cifi� comme un tag HTML
* le lieu o� on veut faire l'affichage (le rendu) est dans le div dont l'identifiant est `p1` (rappel de l'utilisation de `querySelector`: https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelector)

remarque: sur d'ancienne version de React, le style pourrait �tre perdu car `class` est un mot cl� Java et donc dans le JSX, il faudra le remplacer par `className`comme ceci:

```js
function Person(){
  return (
    <div className="person">
      <H1>Max</H1>
      <p>your age : 42</p>
    </div>
  );
}

// rajouter la fonction render
ReactDOM.render(<Person/>, document.querySelector("#p1"));
```

Le r�sultat est:
<img src="img/res2.png" width="50%">

### 2.4 Param�tre d'un composant (ou props)
Dans l'exemple d'avant, nous avons un composant fig�e (nom Max, Age 48). Ce serait bien de pouvoir les param�trer pour cr�er d'autres composants. Pour cela, nous allons utiliser le concept de `props` (pour "properties").

Comment utiliser les `props`pour pouvoir fixer des arguments?
Comme dans tout appel de fonction, les valeurs des arguments sont fix�s lors de l'appel. Il nous faut modifier le code de la fonction comme suit:

```js
function Person(props){
  return (
    <div className="person">
      <h1>{props.name}</h1>
      <p>{props.age}</p>
    </div>
  );
}
```

Cela signifie que nous avons d�fini deux propri�t�s (ou arguments), `name` et `age`. Remarquez la syntaxe avec une seule paire d'accolage `{props.name}` et `{props.age}`.

L'appel se fera en sp�cifiant cette fois-ci la valeur que nous souhaiterons donner � ces `props`que nous venons de d�finir, comme ceci:

et le code d'appel sera

```js
ReactDOM.render(<Person name="Patrick" age="42"/>,
                document.querySelector('#p1'));
```

Mes nouveaux codes:
* rajout d'un nouvel id en HTML (id="p2")
* Appel de render deux fois sur deux instances du composants avec des arguments diff�rents.

![](img/props_code.png)

On remarquera que l'affichage n'est pas comme on l'a sp�cifi� dans le CSS (inline ou en ligne) mais plut�t en bloc (ou passer � la ligne apr�s chaque affichage - c'est � cause du fait qu'un div est toujours par d�faut en affichage block et que le fait de faire le rendu sur 2 div diff�rent, force le html � aller � la ligne (affichage block) m�me si on l'a sp�cifi� dans le css qu'on voulait un inline)

### 2.5 Application au sens React
Dans l'exemple pr�c�dent, nous appelions deux fois la fonction `ReactDOM.render()` pour afficher deux fois le composant.
Pour �viter cela, nous allons modifier notre HTML pour ne pas avoir `id="p1"`et `id="p2"`. Nous allons juste mettre un seul id, appel� arbitrairement `app`.

```html
<div id="app"></div>
```

Nous allons modifier le js en rajoutant une instanciation d'une variable ui contiendra un JSX avec plusieurs instanciation du composant `<Person ... .../>`

```js
function Person(){
  return (
    <div className="person">
      <H1>Max</H1>
      <p>your age : 42</p>
    </div>
  );
}

// rajouter la variable app (ou autre nom)
var mavarJSX =(
  <div>
      <Person name="Patou" age="42"/>
      <Person name="Andr�" age="95"/>
      <Person name="Luc" age="105"/>
  </div>
)
// modifier l'appel afin qu'on n'ait plus qu'un seul render, mais qui rend pas une instance du composant mais la variable qui contient le JSX dans le nouveau div que nous souhaitons utiliser (app)
ReactDOM.render(mavarJSX, 
                document.querySelector('#app'));
```

Le r�sultat est:
![](img/res3.png)

## 3. Pr�vue de la suite:

Ci-dessous la liste des sujets � travailler dans ce cours. 

![](img/course_outiline.png)

## 4.Javascript de nouvelle g�n�ration (optionnel)
Il est important de conna�tre le JS de nouvelle generation (ex: ES6, Arrow function,...) car React est �crit avec ces nouveaut�s. Dans cette partie, nous allons revoir vite fait ces �lements de langage. 
Cette partie est facile � trouver partout sur internet donc elle ne sera pas tr�s d�taill� (mais ce serait bien de finir les challenges)

### 4.1 Comprehension de let et const
`let`, `var` et `const` sont des mani�res de cr�er des variables en JS. `let` et `const` ont �t� introduits dans ES6. 
Comme leur nom l'indique, utiliser `let` pour d�clarer des variables et `const`pour d�clarer des constantes (affect�e une fois et ne change plus). 

Des documents sont � voir [ici](https://www.hackerrank.com/challenges/js10-let-and-const/topics) et des [challenges](https://www.hackerrank.com/challenges/js10-let-and-const/problem?isFullScreen=true) (il faudra ouvrir un compte sur hackerrank.com) 

Exercice: faire le challenge Day0 et Day1 dans hackerrank [10 Days of JS](https://www.hackerrank.com/domains/tutorials/10-days-of-javascript)

### 4.2 Les fonctions fl�ch�es (arrow-functions)
C'est une nouvelle mani�re d'�crire des fonctions en JS. 

La documentation synth�tique est [ici](https://www.hackerrank.com/challenges/js10-arrows/topics) et le challenge est de faire le [Day5]((https://www.hackerrank.com/challenges/js10-arrows/problem?isFullScreen=true) de [10 Days of JS].

D'autres [documentations](https://www.w3schools.com/js/js_arrow_function.asp).

### 4.3 Les imports  et exports
 
Les tutos sur ces �l�ments de langages sont [ici](https://javascript.info/import-export).

NOTE: A regarder sp�cialement les notions suivantes:
* `export/import as`
* `export default` 
* `import` (avec {} et sans {})
* `import *` (comme en Java)
* Comment importer des �l�ments export�s avec `export default` (les noms par d�faut, les exports sans noms)
* importer plusieurs �l�ments diff�rents d'un fichier

Et bien s�r si tout n'est pas clair, voir d'autres tutos pour affiner.

Attention: Tous les navigateurs ne supportent pas toujours les fonctionalit�s des JS de nouvelle g�n�ration.  

### 4.4 Les classes en JS
Idem, nous ne nous attarderons pas, il faudra regarder d'autres cours (ex: [w3schools_inheritance](https://www.w3schools.com/js/js_class_inheritance.asp)). 



Les points � regarder en particuler:
* comment instancier une classe
* l'h�ritage en JS
* les constructeurs en JS - comment appeler un constructeur en cas d'h�ritage ou de red�finition du constructeur (la notion de `super()` comme en C++ ou Java)


Exemple: 
```js
class Person {
  // d�claration d'un constructeur
  constructor(){
    // donne une propri�t�e de la classe
    this.name = "Patou";
  }

  printName(){
    console.log(this.name);
  }

} 

// instanciation de la classe
const pers = new Person();
person.printName();
``` 

On pourrait cr�er une classe `Human` et en faire h�riter `Person`. 
```js
class Human{
  constructor(){
    this.gender='male';
  }
  printGender(){
    console.log(this.gender);
  }
}
// fait h�riter Person de Human
// ce qui donne toutes les props et les
// m�thodes de Human � Person
class Person extends Human{
  // d�claration d'un constructeur
  constructor(){
    // en cas de red�finition du 
    // constructeur en cas d'h�ritage
    super();
    // donne une propri�t�e de la classe
    this.name = "Patou";
  }

  printName(){
    console.log(this.name);
  }

} 

const pers = new Person();
pers.printName();
// fonctionne car Person h�rite de Human
pers.printGender();
```
Tester ce code sur 
Les classes sont importants car elles peuvent �tre utilis�es pour mod�liser la notion de des composants au sens React.

### 4.5 Les propri�t�s et les m�thodes de classes
Il est possible de rajouter � la vol�e des `props` et des `m�thodes` � la classe � la vol�e, directement dans la classe sans le mettre (comme auparavant) dans le constructeur.
Nous allons illustrer l'exemple suivant en le convertissant en classe de JS de nouvelle gen. 

```js
class Human{
  // plus besoin de constructor
  gender = 'male';
  // la fonction a �t� remplac� par la nouvelle syntaxe
  printGender=()=>{
    console.log(this.gender);
  }
}
 
class Person extends Human{
  name = "Patou";
  printName= ()=>{
    console.log(this.name);
  }

} 

const pers = new Person();
pers.printName();
pers.printGender()

```
### 4.6 Les op�rateurs Spread & Rest

On trouve les infos ici: [spread](https://www.w3schools.com/react/react_es6_spread.asp) (peut s'utiliser pour des objets et des tableaux), et l'op�rateur [rest](https://mindsers.blog/fr/post/rest-parameter-et-spread-operator-en-javascript/) (pour avoir des fonctions avec nombre variables d'arguments - en C++ cela equivaut aux variadiques)

Ex:
```js
const numbers =[1,2,3,4];
const newNb=[0,...numbers,5,6,7,8]
console.log(newNb);
```
Donne une sorti comme suit:
```sh
[0, 1, 2, 3, 4, 5, 6, 7]
```
En effet, sans l'op�rateur `Spread` (les 3 points),  on aurait quelque chose comme suit, ce qui ne serait pas correcte:

```js
const numbers =[1,2,3,4];
const newNb=[0,numbers,5,6,7]
console.log(newNb);
```
```sh
[0, [1, 2, 3, 4], 5, 6, 7]
```

L'op�rateur peut fonctionner �galement sur des objets.

```js 
const person={
 nom:"Patou",
 prenom:"Pat"
};

const newPerson={
 ...person,
 age:28
}
console.log(newPerson);
```
Sortie:
```js
[object Object] {
  age: 28,
  nom: "Patou",
  prenom: "Pat"
}
```

### 4.7 Destructuration
Cette op�ration consiste � extraire d'une grosse structure ses �l�ments (ex: tableaux ou objet en variables qui le composent)

La documentation peut se trouver ici: [destructurer](https://www.w3schools.com/react/react_es6_destructuring.asp) et ici [en fran�ais](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment#affecter_avec_un_nom_diff%C3%A9rent)

La destructuration fonctionne �galement pour des objets JS.


### 4.8 Usage par valeur et par r�f�rence

Comme en C++, les types primitives sont sujets � des usages par valeur. 

```js
const num1 = 1 ;
// une nouvelle variable qui contient une copie
// de la valeur de num1
const num2 =num1;
```
Ce n'est pas le cas pour les types d'usage par r�f�rence. 
```js
const person = {
  name:"Patou"
};
// une nouvelle variable mais qui ne fait que 
// r�f�rencer person (ce n'est qu'un pointeur)
const person2= person;
console.log(person.name);
console.log(person2.name);
// je vais changer le nom de person
person.name="Max";
// et je vais r�afficher person2
console.log(person2.name);
```

La sortie montre que le nom associ� � `person2` est aussi chang�. Le type objet a un usage par r�f�rence. 

```sh
"Patou"
"Patou"
"Max"
```

Si toutefois, nous souhaitons copier les valeurs de `person` dans `person2` et cr�er un vrai nouvel objet dans `person2` qui n'est pas un pointeur sur `person`, alors, on peut utiliser l'op�rateur `Spread`(vu pr�c�demment).

```js
const person = {
  name:"Patou"
};
// une nouvelle variable mais qui ne fait que 
// r�f�rencer person (ce n'est qu'un pointeur)

const person2= person;
// devrait afficher Patou
console.log(person.name);
// devrait afficher Patrou
console.log(person2.name);
// changer le nom de person 
// et r�afficher person2
person.name="Max";
// devrait afficher Max car person2 pointe sur 
// person
console.log(person2.name);

// je vais changer le nom de person
const person3 = {
 ...person
}
// changer le nom de person
person.name="Andre";
// et je vais afficher Andre car 
// person2 pointe toujours sur Person
console.log(person2.name);
// affiche toujours "Max" car 
// le nouvel objet est une duplication de person
// originale qui vit maintenant sa vie et n'a /
// pas �t� modifi�
console.log(person3.name);
```
### 4.9 Les m�thodes de gestion de tableaux en js

De la documentation ici [tab_array_method](https://waytolearnx.com/2019/06/10-methodes-de-tableau-dans-javascript-a-connaitre.html).

## V. Workflow de d�veloppement React

### 5.1 Le workflow de developpement
L'objectif est de cr�er un environnement de build. Faire un projet demande plus qu'executer du code sur `www.codepen.io`, donc nous allons monter un environnement.

Pour cela nous devons avoir un environnement qui permet de:
* optimiser nos codes
* executer du js de nouvelles generation (la config babbel par exemple)
* �tre plus productif en utilisant les bons outils (lint par exemple, css auto-prefixing pour la prise en charge de diff�rents navigateurs)

Comment peut-on arriver � ce stade?
* Il nous faudrait avoir un outil de getion de d�p�dance (`yarn`ou `npm`). Ce qu'on appelle `d�pendance` sont les tous les outils/librairies avec des versions sp�cifiques, qui permettent � notre code de fonctionner correctement (`Babbel`, une version sp�cifique de `React`, ...). 
* Il nous faudrait aussi un `Bundler`, qui permet de package plusieurs fichiers (car quand on �crira des fichier de code, ils seront s�par� sur plusieurs fichiers pour se concentrer sur leur propre focus chacun). Dans notre cas `Webpack`(d�bit moyen) sera l'outil que nous choisirons. Pour voir ce que fait un bundler dans la r�alit�, lire ce que fait [webpack dans wikipedia](https://fr.wikipedia.org/wiki/Webpack)
* Nous aurons besoin d'un compilateur comme `Babbel` pour supporter les js de nouvelles g�n�rations.
* un server de dev pour tester notre code.

### 5.1 L'outil "create react app"
C'est un outil qui permet de faire du dev react. 
On peut aller le r�cup�rer [create react app](https://create-react-app.dev/)
Avant d'avancer avec cet outil, il est plus int�ressant d'installer NVM (tel qu'il est d�crit dans [install node version manager](https://heynode.com/tutorial/install-nodejs-locally-nvm/)). Cela permet de ne pas avoir � g�rer les versions diff�rentes de NodeJs. 

Une fois que vous avez install� `NVM`. Cr�er un r�pertoire pour votre developpement React (`~/home/debian/dev_react` - c'est mon chemin local). 
Ensuite,utiliser NVM pour installer une version (ou pla plus r�cente version) de Nodejs.

![](img/install_nodejs.png)

Une fois que vous avez install� nodejs avec nvm, vous avez alors la possibilit� d'utiliser la commande `npm`(Node Package Manager).

Avant de continuer, vous pouvez installer l'outil `yarn` avec la commande ci-dessous comme d�crit dans [install yarn](https://classic.yarnpkg.com/lang/en/docs/install/#windows-stable).

```sh 
debian@debian11: ~/react_dev$ npm install yarn -g
```

Rechercher le package `create-react-app�vec la commande 
```sh 
debian@debian11: ~/react_dev$ npm search create-react-app
```
Il se peut que npm vous propose de mettre � jour votre version de npm avant de pouvoir continuer (lisez bien le retour de la commande)

Tapez la commande suivante pour installer `create-react-app` sur la machine (pas seulement dans le r�pertoire)

```sh 
debian@debian11: ~/react_dev$ npm install create-react-app -g
```
Si vous obtenez un genre d'erreur comme suit:

```sh
npm WARN deprecated tar@2.2.2: This version of tar is no longer supported, and will not receive security updates. Please upgrade asap.
```

alors mettez � jour le package `tar` avec la commande `npm install tar@latest`.

Les commandes lanc�es ci-dessus, auront pour effet de cr�er des fichiers dans le r�pertoire de travail

```sh
debian@debian11:~/react_dev$ ls
node_modules  package.json  package-lock.json
```

Il faudra ensuite cr�er une application `React`avec la commande `create react app` avec la syntaxe suivante: 

`create react app <nom_app> --scripts-version <version>`

NB: l'option `--scripts-version` permet de s'assurer que nous ayons la m�me version de structure de fichier de d�part et non pas chacun diff�rent dans son coin.
Dans notre exemple, nous allons utiliser le nom "react-complet-guide" (comme l'auteur du tuto l'a fait). et une version "1.1.5" de la structure de fichier

```sh
~$ create react app react-complet-guide --scripts-version 1.1.5
```
Cette commande va mouliner et lancer plein d'action (avec �ventuellement des erreurs mais ne pas s'inqui�ter). 

Pour ma part, pas d'erreur, j'ai ceci comme sorti de la commande

![](img/_nouveau_create_react_application.png)

Pour tester le lancement de l'application g�n�r�e, il faut entrer dans le r�pertoire `react-complete-guide` qui a �t� cr��e par la commande et tester le lancement de l'application par `npm start` ou `yarn start`

![](img/lancement_appli_neuf.png)

Le r�sultat permet d'obtenir la fen�tre suivante (la console et une fen�tre Chrome qui contient l'execution en temps r�el de notre application).

![](img/resultat_lancement.png)

Pour l'arr�ter, fermer la fen�tre chrome et taper sur `Ctrl+C` dans la console.

### 5.2 Comprendre la structure de fichiers
Pour la suite, nous allons ouvrir le r�pertoire complet de l'application "react-complet-guide" dans un outil comme `vscode`. 
Voici la structure de fichier qui a �t� g�n�r�e:

![](img/app_file_structure.png)

Nous devrions avoir exactement les m�mes fichiers. 
* Le fichier `package.lock.json`permet de figer des version de d�pendances.

* Le fichier `package.json` nous donne la version des d�pendances que nous utilisons dans le projet:
  - Nous avons 3 d�pendances avec chacun leur versions:
    ```json
    "dependencies": {
      "react": "^18.2.0",
      "react-dom": "^18.2.0",
      "react-scripts": "1.1.5"
    }
    ```
      + `react` est la version de react utilis� pour l'application
      + `react-dom` �galement pour avoir react.
      + `react-scripts` est la version de l'ensemble de script qui nous fournit le workflow qui nous permet d'avoir les commandes `start` , `build`, `test`, ...

* Le r�pertoire `node_modules` contient toutes les d�pendances (et sous-d�pendances) utiles � notre app. Ce r�pertoire ne devrait pas �tre modifi�. 
![](img/node_modules_folder.png)

* Le r�pertoire `public` est le r�pertoire qui est servit par le serveur web � la fin.
![](img/public_folder.png)

  - le fichier `favicon.ico`. 
  Il contient le fichier `favicon.ico` (icon de la page par exemple.) 

  - le fichier `index.html`
    C'est le fichier qui va �tre servit par le serveur web. Nous ne rajouterons pas d'autres fichiers `html` dans ce r�pertoire. Ce fichier `index.html` recevra le code que nous d�velopperons (ce code sera inject� par le workflow de dev dans ce fichier et nous n'avons rien � faire de ce c�t� l�). Dans ce fichier, aucun autre �l�ment html ne sera rajout�. Le fichier contient entre autre, une section comme suit:
      ```html
          <div id="root"></div>
      ```
    C'est l'�l�ment qui servira de point de montage de notre application React plus tard.
    Dans l'en-t�te de ce fichier, cependant, on pourra rajouter des importations de fichiers de style css ou  de m�ta-information.
  - le fichier `manifest.json` contient des m�ta-information (des descriptions typiquement) des �l�ments (ex: ic�nes...) utilis�s par l'appli.
* le r�pertoire `src` contient le code source de notre application. 
![](img/source_folder.png)
On retrouver quelques fichiers tr�s important:
  - le fichier `App.js` qui contient notre application React. Bri�vement, ce fichier contient un composant react �crit en utilisant du JSX.
  - le fichier `index.js`, est le fichier qui fait le lien entre `public/index.html` et notre fichier application `App.js`. 
  En l'occurence, `index.js` donne acc�s � la section identifi�e `root` (dont on parlait plus haut dans le fichier `public/index/html`) afin de faire le rendu de l'applciation `App`avec la m�thode `render()` (d�j� vu en section 2)
  - le fichier `App.css` d�finit quelques styles css de notre application. 
  - le fichier `index.css` qui est encore une feuille style.
  - le fichier `registerServiceWorker.js` est un fichier gen�r� et permet de fournir l'infrastructure n�c�ssaire � la bonne ex�cution de notre code.
  - le fichier `App.test` permet de cr�er des tests unitaires (� voir plus tard)
     ![](img/contenu_index_js1.png)

### 5.3 Premi�re manipulation de l'application
Commen�ons par �diter le fichier `App.js`. 
* Lancez votre application en entrant dans le r�pertoire de l'application que nous avons cr�� en section 5.1 et tapant � la console `npm start` ou `yarn start`. Votre console doit afficher que �a tourne et le serveur web doit tourner dans un navigateur. 

Modifiez votre `App.js` pour ressembler � ceci (supprimer toutes les selectionn�es entre les lignes entre 8 et 16).

![](img/lig_suppr.png)

Remplacer votre code  `App.js` par ceci:

```js
class App extends Component {
  render() {
    return (
      <div className="App">
        <h1>
            Hello, je suis une app React
        </h1>
      </div>
    );
  }
}

export default App;
```
Enregistrez et remarquez que la page se rafra�chit toute seule sans qu'on ait � faire quoi que ce soit (la recompilation est automatique d�s lors qu'on a modifi� notre code).

![](img/exec_app_modifie.png)

Le fichier `logo.svg`, par cons�quence, n'est plus utilis� donc on peut le supprimer (ne pas oublier d'enlever l'appel dans `App.js`)

De la m�me mani�re, nous allons aussi nettoyer le fichier `App.css` pour ne garder que le premier style (le reste est � supprimer)

```css
.App {
  text-align: center;
}
```

La majorit� de notre travail en tant que developpeur React se trouve dans `App.js` ou dans de nouvelles composants React, que nous aurons � cr�er. 

Dans la suite, nous verrons donc un peu plus en profondeur les JSX et comment nous pourrons rajouter plus de composants � notre application React.







