# Ergonomie des formulaires : guider l'utilisateur, simplifier le code

[Les attributs & pseudo-classes associées](#attributs)

[D'autres pseudo-classes utiles](#pseudoClass)

[Les pseudo-éléments](#pseudoElement)

[Les pseudo-éléments généralistes](#generalElement)

## **Les balises HTML** :

|    ** < input type=  ** |   |  **\>  **|
|: :|: :|: :|: :|
|   | Text / Search |   ![](img/input.png)
|    | Number | ![](img/number.png)| *valide si :* (int)
|    | Range | ![](img/range.png) | *min=  max=* | oninput= et < output>\* pour résultat
|    | Radio| ![](img/radio.png)
|    | Checkbox| ![](img/checkbox.png)
|    | Date / Datetime / Datetime-local | ![](img/date.png)  | ![](img/warning-.png) *IE & Firefox* :  pas supporté, sauf date pour Firefox... ![](img/input.png)
|    | Month / Week | ![](img/week.png)  |  ![](img/warning-.png) *IE & Firefox* : pas supportés...  ![](img/input.png)
|    | Time |![](img/time.png) |  ![](img/warning-.png) *IE* : pas supporté...  ![](img/input.png)
|    | Email | ![](img/input.png) |*valide si :* a**@**a
|    | Password | *caractères cachés *  ![](img/password.png)
|    | URL |![](img/input.png) |
|    | File |![](img/file.png) |
|    | Color |![](img/color.png) |
|    | Hidden | *- pour y cacher une valeur par défaut ?*
|    | Button|![](img/button.png) | *value=*
|    | Reset |![](img/reset.png)| *réinitialise tous les champs du formulaire*
|    | Image *src= alt=*|  ![](img/inputImage.png) |  * il s'agit d'un __submit__ graphique : renvoie coordonnées du clic ( / image) *
|    | Submit|![](img/submit.png) |
|    ** < input list=  >**  | < datalist >  * < option>  <òption>* </ datalist > | ![](img/datalist.png) | *liste informative, qui se réduit selon entrées utilisateur*
|**   < button> **| *< img> blabla* | ![](img/buttonTag.png)  | **< /button> **|
|** < select>** | < optgroup label="" > | ![](img/selectOptgroup.png)| < option> </ option> </ optgroup> |** </ select>**
|** < select *multiple* >** | * - size = nb de lignes (multiple ou non) - *| ![](img/selectMultiple.png) | < option> </ option> |** </ select>**
| ** < textarea> ** | *cols= rows=* |  ![](img/textarea.png)| **</ textarea> ** |
| ** < progress> ** |  *value= max=* | ![](img/progress.png)| ** </ progress> ** | *barre remplie de façon dynamique grâce au rapport entre la value et le max*
| ** < meter> ** |  *value= * | ![](img/meter.png) ![](img/warning-.png) *IE * : pas supporté| ** </ meter> ** | *jauge remplie de façon statique, par défaut min=0 et max=1 ; change de couleur si valeur au-delà de high= ou low=* |
|**   * < fieldset> ***  |- *cadre, non interactif* -| ![](img/fieldset.png)| < legend> </ legend>|**   * </ fieldset> ***  |
|**   * < label*** *for=* ***> *** |- *information, non interactif* -| ***</ label>***
|**   * < output >* *** |- *résultat, non interactif* -|**   * < output > *** |

**\*** Exemples d'utilisation d'une balise **< output > : **

pour un calcul :
> < form **oninput = " result.value = **parseInt**(nb1.value) / **parseInt**(nb2.value) "**>

> < input id="nb1"> / < input id="nb2"> = **< output name=**"result" **for=**"nb1 nb2"**>**

pour afficher la valeur d'un range :
> < input type="range" **id="input"**  min="1" max="100" **oninput="output.value = input.value"**>

> **< output id="output"></output>**


## **<a id="attributs">Les attributs HTML et leurs pseudo-classes CSS associées</a>**
Une pseudo-classe CSS se réfère à un état particulier de l’élément, ou à un élément répondant à telle ou telle condition. Parmi les plus connues, il y a les états d’un lien : non visité, survolé, actif, visité, ou encore les nth-child.

La syntaxe est celle-ci :

> *selector**:pseudo-class***   {

> 	 property: value;
> }

Un certain nombre de pseudo-classes sont spécifiques aux éléments de formulaire, d'autres, plus généraux, s'y appliquent particulièrement bien.

![](img/warning-.png) Lorsqu'on stylise la pseudo-classe d'un élément, la mise en forme sur l'élément lui-même n'est pas appliquée (on repart d'une base vierge).

#### autofocus & tabindex=
- **autofocus** : L'élément a le focus au chargement de la page. Attribut sans paramètre.
- **tabindex** : Détermine l'ordre de focus : tabindex=1 tabindex=3 tabindex=2.

Par défaut, le focus *(tab)* suit l'ordre d'apparition des éléments dans le formulaire. Il est très important pour le confort utilisateur de bien penser son ordre de focus.

|-> *A utiliser avec la **pseudo-classe** CSS* **:focus**

#### value="" & placeholder=""
- **value** donne une valeur au champ, comme si l'utilisateur l'avait lui-même entrée, qui sera envoyée avec le formulaire.
- **placeholder** donne une indication à l'utilisateur, sans toucher à la valeur ; il disparaît au premier caractère tapé. Le placeholder n'est jamais envoyé avec le formulaire.

#### checked
Pour les cases à cocher uniquement : case cochée au chargement de la page.
|-> *A utiliser avec la **pseudo-classe** CSS* **:checked**

#### title=""
S'applique à tout élément HTML (sauf range ?) pour faire apparaître une bulle de texte guidant l'utilisateur. Bien utile sur les formulaires lorsque des contraintes ou possibilités spécifiques existent !

#### multiple
Fonctionne avec :
* <**select**>
* < input **type="file"**>
* < input **type="email"**>. Pour entrer plusieurs emails, les séparer d'une virgule. ![](img/warning-.png) Mettre un title pour en informer l'utilisateur !

#### pattern="" , min= , max= , step=
* **pattern** : L'entrée utilisateur doit correspondre à l'expression régulière pour être valide.
> pattern="[0-9]{3}"  pour le code d'un département
* **min**, **max** : *(type="number" ou type="range")* valeurs numériques minimales et maximales autorisées. Sans minimum, les nombres peuvent être négatifs.
* **step** : *(type="number" ou type="range")* 'pas' ou écart entre deux valeurs numériques successives **(conditionne l'incrémentation)**.
> ![](img/warning-.png) min=1 step=2 rendra invalides les nombres pairs rentrés directement par l'utilisateur.

|-> *A utiliser avec les **pseudo-classes** CSS* **:valid** *&* **:invalid** *, et/ou * **:in-range** & **:out-of-range** * qui ne considèrent que le min et max autorisés et non le step ou le pattern.*

![](img/warning-.png) Un champ vide est valide par défaut. ![](img/warning-.png) Ne pas utiliser seul : les éléments non formulaire sont considérés aussi, avec des résultats variés.

#### maxlength=""
Bloque en écriture lorsque le nombre de caractères est atteint.

#### autocomplete=
Suggère une donnée entrée précédemment lorsque la/les première(s) lettres correspondent.
Deux valeurs possibles : **on** ou **off**. Peut s'appliquer au formulaire dans son intégralité et/ou à un champ particulier.

#### required & optional
* **required** : si l'utilisateur ne donne pas de valeur au champ, empêche l'envoi (message).
* **optional** : par défaut ; vide, le champ n'empêche pas l'envoi.

|-> *A utiliser avec les **pseudo-classes** CSS* **:required** *&* **:optional**

#### disabled & readonly
* **disabled** : empêche l'interaction utilisateur sur l'élément. Par défaut le bouton ou le champ est grisé. Aucune valeur ne sera envoyée. Tab ne lui donnera pas le focus.
* **readonly** : empêche l'utilisateur de modifier la valeur de l'élément, mais elle sera bel et bien envoyée avec le formulaire. Tab lui donnera le focus. Grisé par défaut. Ne fonctionne pas avec < select > < button > < option >.

|-> *A utiliser avec les **pseudo-classes** CSS* **:disabled** *&* **:enabled**.

![](img/warning-.png) La pseudo-classe **:read-only** ou **:-moz-read-only** ne concerne que quelques navigateurs. Sa contraire **:read-write** est mieux supporté, mais pas par IE, et elle ne concerne que les input text (et textarea).

#### hidden
L'attribut **hidden** glissé dans un tag équivaut au css **display: none;** ![](img/warning-.png) (voir ci-après).

### Les attributs du formulaire
#### target=""
Détermine où afficher la réponse serveur après soumission du formulaire. Comme pour les liens, peut prendre les valeurs :
* **\_blank** (nouvel onglet ou page)
* **\_self** (iframe/page actuelle, par défaut)
* **iframe_name** (s'affiche dans l'iframe nommé)


## **<a id="pseudoClass">Les pseudo-classes généralistes</a>** :

#### :hover
Au survol : outre un changement d'apparence, hover peut par exemple permettre de styliser une "infobulle" maison :

> p {

>      display: none;
}

> div**:hover** p {

>      display: block;
}

###### *Note : *visibility: hidden; & display: none;
Ces propriétés CSS sont extrêmement utiles pour cacher une partie du formulaire qui ne concerne que certaines situations, et la faire réapparaître si l'utilisateur a entré des données qui la rendent pertinente (exemple : renseignements sur les enfants inutiles si on a zéro enfant).

* **visibility:hidden** : on ne voit plus l'élément ni ses enfants, par contre la place est toujours prise. Pour le faire réapparaître on utilise **visibility:visible**.
* **display:none** : l'élément est retiré avec ses enfants, le reste du code remonte de façon à prendre sa place. L'élément n'est cependant pas détruit et on peut le rétablir à tout moment grâce à un display approprié : **display:flex|inline|block|....**

#### :active
Au clic : comme hover, peut (fugacement) modifier ou faire apparaître quelque chose (l'image du bouton cliqué). Moins durable...

#### :lang()
Si on a renseigné dans des tags l'**attribut lang=""** (fr, en, fr-FR, en-US, ru, en...), on peut cibler ces éléments en css grâce à la pseudo-class **:lang()**

> < html **lang="fr"**> < blockquote **lang="en"**> *A person who never made a mistake never made anything new.* < /blockquote>

> < style> **:lang(en)**  {  font-style: italic;   } < /style>

*Note* : :lang(fr) trouve les lang="fr" et les lang="fr-FR").

### Cibler certains éléments selon leur ordre, type, enfants...
#### :first-child, :nth-child(), :last-child
Cible le premier, le nième, le dernier enfant de l'élément, mais aussi :
* les enfants pairs **:nth-child(even)**
* les enfants impairs **:nth-child(odd)**
* tous les trois enfants en commençant par le premier **:nth-child(3n+1)** - ou autre

#### :first-of-type, :nth-of-type(), :last-of-type, :nth-last-of-type(), only-of-type
De la même manière que les -child, cible le premier, le nième, le dernier élément du type indiqué, pour chaque niveau :
* par exemples les lignes paires de chaque tableau : tr:**nth-of-type(even)**
* **:nth-last-of-type(2)** : l'avant-dernier du type (par exemple avec des li, si le dernier est simplement informatif)
* input[type="option"]**:only-of-type** : seulement s'il est le seul élément de ce type à un niveau donné

#### :not()
Sélectionne tout ce qui n'est pas... ![](img/warning-.png) il faut avoir stylisé les propriétés de l'élément pour que les mêmes propriétés ne s'appliquent qu'aux non-éléments.

    input:[type="text"]
      {
        ma_propriété: valeur;
      }

    input:not( [type="text"] )
      {
        ma_propriété: autre_valeur;
      }

#### :empty
![](img/warning-.png) Ne désigne pas un champ sans valeur mais un **élément sans innerHTML**, en dur dans le code :

* Un paragraphe pour être *empty* ne doit contenir ni balises ni texte.
* Un textarea vide dans le code reste *empty* quand l'utilisateur le remplit.
* Un élément sans balise fermante ne peut être qu'*empty*.

#### :link
Lien.

#### :root
Sélectionne la racine du document, c'est-à-dire la balise html. C'est une équivalence stricte. Dans d'autres langages, ça peut être différent.

Utilité : définir la taille de base, en pixels, des polices de caractères, permettant de calibrer son "em".
> :root { font-size: 10px; }

> div { width: 60em; }

## **<a id="pseudoElement">Les pseudo-éléments</a>**
Contrairement aux pseudo-classes, les pseudo-éléments en HTML5 sont annoncés par **deux ::**. Ce sont des éléments sans balise, soit qui s'ajoutent (::before & ::after), soit qui délimitent une partie du contenu d'une balise.

Il n'y a que cinq pseudo-éléments généralistes ; **les pseudo-éléments de formulaire ne sont pas standards** et dépendent donc des navigateurs.

Les éléments de formulaire ont tous une apparence différente selon le navigateur, et leurs pseudo-classes sont appelées différemment. Les préfixes à utiliser sont **-moz-** pour Firefox, **-webkit-** pour Safari et Chrome, **-o-** pour Opera et **-ms-** pour Internet Explorer. Parfois, l'appellation sans préfixe sera utilisée par tel ou tel navigateur. Mieux vaut vérifier avant de se lancer.

Jouer avec ces pseudo-éléments de formulaire permet d'homogénéiser autant que personnaliser ces apparences par défaut. Pour **enlever toutes les valeurs de l'apparence par défaut** :
> form * {

>  &nbsp; &nbsp; **-webkit-appearance: none;** // Chrome,

>  &nbsp; &nbsp;  **-moz-appearance:    none;**

>  &nbsp; &nbsp;  **appearance:         none;**

> }

Pour aller plus loin : [reset CSS](https://gist.github.com/anthonyshort/552543)
#### input::-moz-focus-inner, input::-moz-focus-outer
Sous Firefox, l'élément qui a le focus est entouré d'une bordure en pointillé que l'on peut retirer ( border: none; ).

#### Exemple des pseudo-éléments pour input range :
> ::-webkit-slider-runnable-track / ::-moz-range-track / ::-ms-track

> ::-webkit-slider-thumb / ::-moz-range-thumb / ::-ms-thumb

Le track est la barre, le thumb le curseur. Si l'on veut styliser les deux éléments, il faut également penser à les styliser en :hover :focus et :active. Voici comment les pseudo-classes et éléments peuvent s'enchaîner :

> input[type=range]**:hover::-webkit-slider-thumb:before**

 ![](img/warning-.png) Consulter la documentation des navigateurs pour connaître tous les pseudo-éléments d'un type d'élément de formulaire donné.


### **<a id="generalElement">Pseudo-éléments généralistes</a>** :

#### ::selection
Ce qui est sélectionné par l'utilisateur.

#### ::before & ::after
La seule propriété indispensable de ces pseudo-éléments, c'est **content=**;, que l'on peut remplir avec :
> une chaîne de caractère (avec guillemets) : **content: "";**  ou **content: "Note: ";**

> une image (sans guillemets) : **content: url(**icon.png**);**

> un compteur de liste (sans guillemets) :  **content: counter(**var**)**;

Si l'on veut mettre plusieurs éléments (compteur et texte par ex), on les sépare juste d'un espace :

> ul {

> &nbsp; &nbsp; &nbsp; &nbsp; **counter-reset**: chap; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; * // initialise le compteur : on le place au niveau du parent des entrées de la liste, et on lui donne un nom (ici chap) *

> }

> li::before {

> &nbsp; &nbsp; &nbsp; &nbsp; counter-increment: chap;  &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; *// incrémente le compteur*

> &nbsp; &nbsp; &nbsp; &nbsp; content: **url(**puce.png**) "** chapitre **" counter(**chap**)**; &nbsp; &nbsp; &nbsp; *// donne : ** chapitre 1 *

> }

Ces pseudo-éléments sont **par défaut en display: inline;**. Pour les dimensionner et les positionner autrement, il faudra changer pour du **display: inline-block; ou du display: block;.**

#### ::first-letter & ::first-line
Comme pour le ::before ou ::after, si l'on souhaite changer les dimensions ou la position de la première lettre/ligne, il faudra changer son display (par défaut inline).
