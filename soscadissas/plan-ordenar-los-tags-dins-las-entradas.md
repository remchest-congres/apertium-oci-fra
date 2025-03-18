# Faire attention à l'ordre des tags dans les entrées du dictionnaire

Pour que les dictionnaires monolingues d'apertium puissent produidre une forme de surface à partir d'un lemme et de catégories (et autres étiquettes) données il faut que ces étiquettes soient renseignées dans un ordre bien précis.

Si les tags n'arrivent pas dans le bon ordre alors le dictionnaire monoligue ne pourra pas produire la forme de surface.

## Un exemple

Pour illustrer ce problème je vais prendre l'exemple d'une traduction du mot `sorcières` dans le sens français -> occitan. En sortie on veut que la traduction produise `mascas` en languedocien et `broishas` en gascon. 

En français le lemme de "sorcier" est le même pour ses formes singulier, plurier, masculin et féminin.

Les entrées dans le dictionnaires bilingue vont donc ressembler à ça :

```xml
<e><p><l>masc<s n="n"/></l>             <r>sorcier<s n="n"/></r></p><par n="d:lengadocian"/></e>
<e><p><l>broish<s n="n"/></l>           <r>sorcier<s n="n"/></r></p><par n="d:gascon"/></e>
```

- Ici les entrées portent juste l'information que le mot concerné est un nom. Le genre et le nombre ne sont pas renseignés car ces entrées doivent être appelées dans les 4 cas possibles (m/sg - f/sg - m/pl - f/pl) 
- Le dictionnaire monolingue français est en charge de rajouter les tags correspondant au genre et au nombre
- Les tags `d:lengadocian` et `d:gascon` sont des paradigmes simples permettant de désambiguiser en fonction de l'un ou l'autre des dialèctes

## Le problème

Le problème avec cette définition est que la commande :

```sh
$ echo 'sorcières' | apertium -d . fra-oci-biltrans
```

Produira la sortie :

```^sorcier<n><f><pl>/masc<n><d:lengadocian><f><pl>/broish<n><d:gascon><f><pl>$```

Or la forme :

```/masc<n><d:lengadocian><f><pl>```

Ne peut pas être produite par le dictionnaire monolingue occitan car celui-ci s'attends à ce que les trois premiers tags soient (dans cet ordre) :

1. la nature (PoS)
2. le genre 
3. le nombre

Pour que cela fonctionne il faut que `fra-oci-biltrans` renvoie quelque chose comme :

```/masc<n><f><pl><d:lengadocian>```

Source : [documentation apertium](https://wiki.apertium.org/wiki/Tag_order)

## Solution

Il faut donc s'assurer que le tag identifiant un dialècte soit forcément placé à la fin de la définition, et ce même dans le cas ou des tags de genre et de nombre seraient rajoutés automatiquement à la suite de la nature.

Un solution est donc de passer par un paradigme permettant de gérer les tags de nature/genre/nombre pour les entrées qui regroupent masculin/féminin et singulier/pluriel :

```xml
<pardef n="t:nom_masculin_feminin">
    <e><p><l><s n="n"/><s n="f"/><s n="sg"/></l>         <r><s n="n"/><s n="f"/><s n="sg"/></r></p></e>
    <e><p><l><s n="n"/><s n="f"/><s n="pl"/></l>         <r><s n="n"/><s n="f"/><s n="pl"/></r></p></e>
    <e><p><l><s n="n"/><s n="m"/><s n="sg"/></l>         <r><s n="n"/><s n="m"/><s n="sg"/></r></p></e>
    <e><p><l><s n="n"/><s n="m"/><s n="pl"/></l>         <r><s n="n"/><s n="m"/><s n="pl"/></r></p></e>
</pardef>
```

Ce paradigme indique simplement de faire correspondre les tags arrivant de la langue de gauche avec la langue de droite et inversement.

La définition dans notre dictionnaire bilingue deviens donc :

```xml
<e><p><l>masc</l>         <r>sorcier</r></p><par n="t:nom_masculin_feminin"/><par n="d:lengadocian"/></e>
<e><p><l>broish</l>       <r>sorcier</r></p><par n="t:nom_masculin_feminin"/><par n="d:gascon"/></e>
```

- On à retiré l'information du nom des deux côtés, celle-ci sera gérée par le paradigme `t:nom_masculin_feminin`.

Ainsi lorsque le dictionnaire français reconnaitra :

```sorcier<n><f><pl>```

Alors le dictionnaire bilingue retournera : 

```^sorcier<n><f><pl>/masc<n><f><pl><d:lengadocian>/broish<n><f><pl><d:gascon>$```

Et le dictionnaire monolingue occitan sera à même de réaliser la ou les formes demandées.

## Remarque

Cette solution ne semble pas idéale. Bien qu'elle permette de contourner le problème elle risque dans le même temps de mener à une multiplication imprévue du nombre de paradigmes dans le dictionnaire bilingue.

Pour autant il semble impossible à cause du fonctionnement d'apertium d'avoir un ordre variable des tags et je n'ai pour l'instant pas trouvé de moyens réorganiser l'ordre des tags en entré ou en sortie d'un dictionnaire. 

# Code final

Voici l'ensemble des définitions pour la solution proposée ci-dessus :

## Dictionnaire bilingue `apertium-oci-fra.oci-fra.dix`

```xml
<dictionary>
    ...
    <sdefs>
        ...
        <sdef n="d:gascon" c="mot del dialècte Gascon"/>
        <sdef n="d:lengadocian" c="mot del dialècte Lengadocian"/>
    </sdefs>

    <pardefs>
        <!-- ********** d: paradigmes de dialectes ********** -->

        <pardef n="d:gascon">
            <e r="LR"><p><l></l><r></r></p></e>
            <e r="RL"><p><l><s n="d:gascon"/></l><r></r></p></e>
        </pardef>

        <pardef n="d:lengadocian">
            <e r="LR"><p><l></l><r></r></p></e>
            <e r="RL"><p><l><s n="d:lengadocian"/></l><r></r></p></e>
        </pardef>

        <!--  ********** t: paradigmes que fan sonque apondre de tags ********** -->

        <pardef n="t:nom_masculin_feminin">
            <e><p><l><s n="n"/><s n="f"/><s n="sg"/></l>         <r><s n="n"/><s n="f"/><s n="sg"/></r></p></e>
            <e><p><l><s n="n"/><s n="f"/><s n="pl"/></l>         <r><s n="n"/><s n="f"/><s n="pl"/></r></p></e>
            <e><p><l><s n="n"/><s n="m"/><s n="sg"/></l>         <r><s n="n"/><s n="m"/><s n="sg"/></r></p></e>
            <e><p><l><s n="n"/><s n="m"/><s n="pl"/></l>         <r><s n="n"/><s n="m"/><s n="pl"/></r></p></e>
        </pardef>
    </pardefs>

    <section id="main" type="standard">
        <e><p><l>masc</l>         <r>sorcier</r></p><par n="t:nom_masculin_feminin"/><par n="d:lengadocian"/></e>
        <e><p><l>broish</l>       <r>sorcier</r></p><par n="t:nom_masculin_feminin"/><par n="d:gascon"/></e>
    </section>
</dictionary>
```

## Dictionnaire monolingue Occitan `apertium-oci.oci.metadix`

```xml
<dictionary>
    ...
    <pardefs>
        ...

        <!--  ********** p: paradigmes simples ********** -->

        <!-- Mots que prenon una 's' al plural -->
        <pardef n="p:s_plural">
            <e><p><l></l>         <r><s n="sg"/></r></p></e>
            <e><p><l>s</l>        <r><s n="pl"/></r></p></e>
        </pardef>

        ...

        <!--  ********** t: paradigmes que fan sonque apondre de tags ********** -->

        <!-- Apond los tags per un nom feminin -->
        <pardef n="t:nom_feminin">
            <e><p><l></l>         <r><s n="n"/><s n="f"/></r></p><par n="p:s_plural"/></e>
        </pardef>

        <!-- Apond los tags per un nom masculin -->
        <pardef n="t:nom_masculin">
            <e><p><l></l>         <r><s n="n"/><s n="m"/></r></p><par n="p:s_plural"/></e>
        </pardef>

        ...

        <!-- ********** a: paradigme agrégat ********** -->

        <!-- Mots masculins/feminins que s'acaban per una 'a' al feminin -->
        <pardef n="a:nom_M/F_amb_la_terminasion_A_al_feminin">
            <e><p><l></l>         <r></r></p><par n="t:nom_masculin"/></e>
            <e><p><l>a</l>        <r></r></p><par n="t:nom_feminin"/></e>
        </pardef>
    </pardefs>

    <section id="main" type="standard">
        <e lm="masc"><i>masc</i><par n="a:nom_M/F_amb_la_terminasion_A_al_feminin"/></e>
        <e lm="broish"><i>broish</i><par n="a:nom_M/F_amb_la_terminasion_A_al_feminin"/></e>
    </section>
</dictionary>
```

