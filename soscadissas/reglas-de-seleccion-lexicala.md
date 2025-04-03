# Adaptation des règles de sélection lexicales

## Problematique

Avec le nouveau système de variations on ne peut plus utiliser l'attribut `v` (`v="oci"`, `v="oci@gascon"`, ...) dans les règles de sélection lexicales (<b>LRX</b>).
Il faut donc trouver un moyen pour qu'une règle puisse produire deux sorties differentes en fonction des paramètres de variations.

Le problème est que, en dehors du cas de l'utilisation de l'attribut `v`, la balise `match` d'une LRX ne peut accepter qu'une seule balise `select` (ou `remove`).

On ne peut donc pas se contenter de remplacer :

```xml
<rule weight="0.8">
    <match lemma="enjamber" tags="vblex.*" v="oci"><select lemma="enforcar"/></match>
    <match lemma="enjamber" tags="vblex.*" v="oci@gascon"><select lemma="en·horcar"/></match>
</rule>
```

Par quelque chose comme :

```xml
<rule weight="0.8">
    <match lemma="enjamber" tags="vblex.*"><select lemma="enforcar" tags="*.d:lengadocian.*"/></match>
    <match lemma="enjamber" tags="vblex.*"><select lemma="en·horcar" tags="*.d:gascon.*"/></match>
</rule>
```

Car le Apertium refusera de compiler une règle contenant deux `select`.

## Solution

Voici une solution possible que j'ai trouvé. L'idée ici est que plutôt que d'avoir une règle prenant en compte toutes les variétés, on va plutôt définir une règle pour chacune des variétés concernée. 

Le choix de la règle à utiliser sera en fait determiné <b>en amont</b> par le l'étape de désambiguisation avant transfert du dictionnaire bilingue (rlx). 

## Exemple

Voilà donc un exemple pour y voir plus clair.

### Jeux de données

Pour cet exemple on va prendre le cas de la règle `enjamber -> enforcar/encambar` dont les différents cas métiers sont résumés dans ce tableau :

|  | traduction par défaut de "enjamber" | "enjamber" suivit de "un vélo" |
| --- | --- | --- |
| <b>languedocien</b> | enforcar | encambar |
| <b>gascon</b> | en·horcar | encamar |

<details>
    <summary><b>Règle correspondante dans la version actuelle d'apertium</b></summary>


```xml
<rule weight="0.8">
    <match lemma="enjamber" tags="vblex.*" v="oci">
        <select lemma="enforcar"/>
    </match>
    <match lemma="enjamber" tags="vblex.*" v="oci@gascon">
        <select lemma="en·horcar"/>
    </match>
</rule>
<rule weight="1.0">
    <match lemma="enjamber" tags="vblex.*" v="oci">
        <select lemma="encambar"/>
    </match>
    <match lemma="enjamber" tags="vblex.*" v="oci@gascon">
        <select lemma="encamar"/>
    </match>
    <repeat from="0" upto="2">
        <match tags="adv"/>
    </repeat>
    <match tags="det.*"/>
    <or>
        <match lemma="vélo" tags="n.*"/>
        <match lemma="bicyclette" tags="n.*"/>
        <match lemma="cheval" tags="n.*"/>
    </or>
</rule>
```

</details>

### Données dans le dictionnaire bilingue

```xml
<e><p><l>enforcar<s n="vblex"/></l>                             <r>enfourcher<s n="vblex"/></r></p><par n="d:lengadocian"/></e>
<e><p><l>en·horcar<s n="vblex"/></l>                            <r>enfourcher<s n="vblex"/></r></p><par n="d:gascon"/></e>

<e><p><l>enforcar<s n="vblex"/></l>                             <r>enjamber<s n="vblex"/></r></p><par n="d:lengadocian"/></e>
<e><p><l>encambar<s n="vblex"/></l>                             <r>enjamber<s n="vblex"/></r></p><par n="d:lengadocian"/></e>

<e><p><l>en·horcar<s n="vblex"/></l>                            <r>enjamber<s n="vblex"/></r></p><par n="d:gascon"/></e>
<e><p><l>encambar<s n="vblex"/></l>                             <r>enjamber<s n="vblex"/></r></p><par n="d:gascon"/></e>

<e><p><l>un<s n="det"/><s n="ind"/><s n="m"/><s n="sg"/></l>    <r>un<s n="det"/><s n="ind"/><s n="m"/><s n="sg"/></r></p></e>
<e><p><l>velo<s n="n"/><s n="m"/></l>                           <r>vélo<s n="n"/><s n="m"/></r></p></e>
```

### Nouvelles règles

Ici la solution consiste donc a définir les trois règles suivantes :

<details>
    <summary><b>Remarque 1</b></summary>
    
On remarquera ici qu'aucune des règles ne porte la notion de dialecte ou de variante. Comme je l'ai dit dans la présentation de la solution, ce choix est délégué au fichier `.rlx`. Pour plus de détails, voir le point suivant : [Explication](#explication).

</details>
<br/>

<b>Règle 1</b> : définit la traduction par défaut pour le languedocien

```xml
<rule weight="0.8">
    <match lemma="enjamber" tags="vblex.*">
        <select lemma="enforcar" />
    </match>
</rule>
```
<b>Règle 2</b> : définit la traduction par défaut pour le gascon

```xml
<rule weight="0.8">
    <match lemma="enjamber" tags="vblex.*">
        <select lemma="en·horcar" />
    </match>
</rule>
```

<b>Règle 3</b> : définit la traduction dans le cas ou `enjamber` serait suivit de `un vélo`.
    
<details>
    <summary><b>Remarque 2</b></summary>
    
Je précise qu'ici il y a une règle commune pour les deux dialètes car, dans mes données de test du dictionnaire monolingue occitan, le lemme `encambar` peux produire les deux formes `encambar` et `encamar` grâce à un paradigme `p:casuda_b`. 

Dans un autre cas ou les lemmes seraient différents pour les deux dialectes il faudrait dupliquer cette règle comme cela a été fait pour les règles 1 et 2.

</details>
<br/>

```xml
<rule weight="1.0">
    <match lemma="enjamber" tags="vblex.*">
        <select lemma="encambar" />
    </match>
    <repeat from="0" upto="2">
        <match tags="adv"/>
    </repeat>
    <match tags="det.*"/>
    <or>
        <match lemma="vélo" tags="n.*"/>
        <match lemma="bicyclette" tags="n.*"/>
        <match lemma="cheval" tags="n.*"/>
    </or>
</rule>
```

### Explication

Voila ce qui se passe étapes par étapes dans le cas où ont entre la commande suivante :

```sh
$ echo "enjamber un vélo" | apertium -d . fra-oci
```

Initialement le dictionnaire bilingue va rechercher les correspondances pour `enjamber` et trouver une quadruple ambiguité `enforcar(lengadocian)`/`encambar(lengadocian)`/`encambar(gascon)`/`en·horcar(gascon)`.

Le fichier `fra-oci.biprefs.rlx` va ensuite désambiguiser en fonction du mode selectionné pour la traduction. Ici il va donc retirer les entrées correspondant au gascon et retourner une double ambiguité `enforcar(lengadocian)`/`encambar(lengadocian)` :

```sh
$ echo "enjamber un vélo" | apertium -d . fra-oci-biprefs
^enjamber<vblex><inf>/enforcar<vblex><d:lengadocian><inf>/encambar<vblex><d:lengadocian><inf>/¬encambar<vblex><d:gascon><inf><REMOVE:6>/¬en·horcar<vblex><d:gascon><inf><REMOVE:6>$ ^un<det><ind><m><sg>/un<det><ind><m><sg>$ ^vélo<n><m><sg>/velo<n><m><sg>$
```

Enfin les règles LRX sont appliquées :

- La <b>règle 1</b> matche et sélectionne le lemme `enforcar`
- La <b>règle 2</b> matche mais ne selectionne rien car il n'y a déjà plus de lemme `en·horcar` dans le stream
- La <b>règle 3</b> matche et sélectionne le lemme `encambar`. Ayant un poids plus important que la règle 1, elle passera donc en priorité et écrasera la sélection précédente.

On obtient donc en sortie :

```sh
echo "enjamber un vélo" | apertium -d . fra-oci-lex_v
2:SELECT:1:enjamber<vblex><inf>:2:encambar<vblex><d:lengadocian><inf>
^enjamber<vblex><inf>/encambar<vblex><d:lengadocian><inf>$ ^un<det><ind><m><sg>/un<det><ind><m><sg>$ ^vélo<n><m><sg>/velo<n><m><sg>$
```

### Sorties

Voici l'ensembles des sorties produites par cet exemple 

```sh
$ echo "enjamber un vélo" | apertium -d . fra-oci
encambar un velo
$ echo "enjamber" | apertium -d . fra-oci
enforcar
$ echo "enjamber un vélo" | apertium -d . fra-oci_gascon
encamar un velo
$ echo "enjamber" | apertium -d . fra-oci_gascon
en·horcar
```

## Remarque additionelle

### Avoir une entrée pour chaque dialecte

Dans les données du dictionnaire bilingue de l'exemple présenté ci-dessus, on notera que la paire de traduction `encambar <-> enjamber` est présente deux fois, une pour chaque dialecte. Et ce malgré le fait que dans le dictionnaire monolingue occitan le lemme `encambar` puisse produire à la fois la forme gascone et la forme languedocienne. 

Ceci est dû au fait que le fichier `fra-oci.biprefs.rlx` désambiguise avant notre fichier `.lrx`.

Dans l'idée on aimerai avoir ici une seule entrée pour les deux dialectes, pour ce faire on aurait deux solutions envisageables mais aucune des deux ne peut fonctionner.

#### Solution 1 : une entrée sans paradigme de dialecte

```xml
<e><p><l>encambar<s n="vblex"/></l>     <r>enjamber<s n="vblex"/></r></p></e>
```

Dans cette solution on envisage une entrée qui serait commune à l'ensemble des variations de l'occitan. Le problème est que dans ce cas, le fonctionnement du fichier `fra-oci.biprefs.rlx` fait que c'est cette entrée qui sera toujours choisie.

Dans le cas d'une traduction dans le mode par défaut `fra-oci` sans aucune variable passée en entrée voila ce que ça donnerai :

1) le dictionnaire bilingue trouve une triple ambiguité `enforcar(lengadocian)`/`encambar`/`en·horcar(gascon)`
2) le fichier `fra-oci.biprefs.rlx` applique ses règles :
    
    1) la première règle retire les mots gascons
        ```
        SELECT (d:gascon)      IF (0 (VAR:gascon)) ;
        REMOVE (d:gascon) ;
        ```
        Il reste `enforcar(lengadocian)`/`encambar`
    2) la deuxième règle retire les mots languedociens
        ```
        SELECT (d:lengadocian)      IF (0 (VAR:lengadocian)) ;
        REMOVE (d:lengadocian) ;
        ```
        Il reste `encambar`

3) le fichier `.lrx` est appelé mais il n'y a plus rien a désambiguiser, c'est donc `encambar` qui est choisi indépendamment de la LRX qu'on cherche à appliquer

#### Solution 2 : une entrée avec les deux paradigmes de dialecte

```xml
<e><p><l>encambar<s n="vblex"/></l>     <r>enjamber<s n="vblex"/><par n="d:lengadocian"/><par n="d:gascon"/></r></p></e>
```

Dans cette solution j'ai voulu indiquer une seule entrée ayant les paradigmes des deux dialectes. Mais le problème dans ce cas est que, pour une traduction dans le mode par défaut `fra-oci` sans aucune variable passée en entrée, cette entrée sera toujours supprimée par le fichier `fra-oci.biprefs.rlx` :

1) le dictionnaire bilingue trouve une triple ambiguité `enforcar(lengadocian)`/`encambar(lengadocian|gascon)`/`en·horcar(gascon)`
2) le fichier `fra-oci.biprefs.rlx` applique ses règles :
    
    1) la première règle retire les mots gascons
        ```
        SELECT (d:gascon)      IF (0 (VAR:gascon)) ;
        REMOVE (d:gascon) ;
        ```
        Il reste `enforcar(lengadocian)`
    2) Il n'y a plus d'ambiguité donc on ne va pas jusqu'à l'application de la règle 2
        ```
        SELECT (d:lengadocian)      IF (0 (VAR:lengadocian)) ;
        REMOVE (d:lengadocian) ;
        ```
        Il reste `enforcar(lengadocian)`

3) le fichier `.lrx` est appelé mais il n'y a plus rien a désambiguiser, c'est donc `enforcar(lengadocian)` qui est choisi indépendamment de la LRX qu'on cherche à appliquer.

Dans le cas d'une traduction avec le mode `fra-oci_gascon`, sela fonctionnera comme attendu :

1) le dictionnaire bilingue trouve une triple ambiguité `enforcar(lengadocian)`/`encambar(lengadocian|gascon)`/`en·horcar(gascon)`
2) le fichier `fra-oci_gascon.biprefs.rlx` applique sa règles :
    
    1) la première règle sélectionne les mots gascons
        ```
        IFF (d:gascon);
        ```
        Il reste `enforcar(lengadocian)`/`encambar(lengadocian|gascon)`

3) le fichier LRX est appelé et applique notre règle.

### Règles negatives

Au besoin et en fonction des cas métiers on peut aussi voir les règles dans l'autre sens, c'est à dire en suppression plutôt qu'en sélection.

Ainsi le groupe de règles ci-dessous est équivalent au groupe de règles présenté en exemple :

```xml
<rule weight="0.8">
    <match lemma="enjamber" tags="vblex.*">
        <remove lemma="encambar"/>
    </match>
</rule>

<rule weight="1.0">
    <match lemma="enjamber" tags="vblex.*">
        <remove lemma="enforcar"/>
    </match>
    <repeat from="0" upto="2">
        <match tags="adv"/>
    </repeat>
    <match tags="det.*"/>
    <or>
        <match lemma="vélo" tags="n.*"/>
        <match lemma="bicyclette" tags="n.*"/>
        <match lemma="cheval" tags="n.*"/>
    </or>
</rule>

<rule weight="1.0">
    <match lemma="enjamber" tags="vblex.*">
        <remove lemma="en·horcar"/>
    </match>
    <repeat from="0" upto="2">
        <match tags="adv"/>
    </repeat>
    <match tags="det.*"/>
    <or>
        <match lemma="vélo" tags="n.*"/>
        <match lemma="bicyclette" tags="n.*"/>
        <match lemma="cheval" tags="n.*"/>
    </or>
</rule>
```
