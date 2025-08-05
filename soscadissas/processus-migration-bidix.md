# prérequis

- [x] mise en place des tests de non régression (en local)
- [x] setup d'une branche de migration
- [x] sur la branche de migration, restaurer l'ensemble des fichiers à leurs états précédents (état du répo courrant d'apertium)
- [x] vérifier la pertinance de travailler sur les fichiers `apertium-oci-fra.fra-oci.t2x_supersn` et `apertium-oci-fra.fra-oci.t2x_enon`
  - ces fichiers sont du WIP abandonné (donc dépréciés)

# modifications sur la structure des fichiers

## chunking rules

séparer les fichiers de chunk en deux : un fichier par variété contenant les règles spécifiques a la variété ET les règles communes.

mettre à jour le Makefile.am

mettre à jour les modes

### files

- [x] apertium-oci-fra.fra-oci.t1x
- [x] apertium-oci-fra.oci-fra.t1x

## interchunks

séparer chaque fichier interchunk en 3 fichiers distincts :

- l'un concernant les règles du gascon
- l'un concernant les règles du lengadocian
- le dernier concernant les règles communes

puis dans chaque mode on appelle le fichier de la variété suivit du fichier commun

mettre à jour le Makefile.am

mettre à jour les modes

### files

- [x] ~~apertium-oci-fra.oci-fra.t2x_temps~~ ne dépend pas des variétés
- [x] apertium-oci-fra.oci-fra.t2ax
- [x] apertium-oci-fra.oci-fra.t2ax2
- [x] apertium-oci-fra.oci-fra.t2bx
- [x] apertium-oci-fra.oci-fra.t2cx
- [x] ~~apertium-oci-fra.oci-fra.t2dx~~ ne dépend pas des variétés
- [x] ~~apertium-oci-fra.oci-fra.t2ex~~ ne dépend pas des variétés
- [x] ~~apertium-oci-fra.oci-fra.t2x_temps~~ ne dépend pas des variétés
- [x] ~~apertium-oci-fra.fra-oci.t2x_ini~~ ne dépend pas des variétés
- [x] apertium-oci-fra.fra-oci.t2x
- [x] apertium-oci-fra.fra-oci.t2x_bis
- [x] ~~apertium-oci-fra.fra-oci.t2x_pas~~ ne dépend pas des variétés
- [x] ~~apertium-oci-fra.fra-oci.t2x_pro~~ ne dépend pas des variétés
- [ ] ~~(apertium-oci-fra.fra-oci.t2x_supersn)~~
- [ ] ~~(apertium-oci-fra.fra-oci.t2x_enon)~~

## postchunks

les fichiers postchunk ne sont pas dépendant des variétés

## final transfer rules

les règles finales de transfert ne sont pas impactés par la notion de variétés

## multiwords

pour chaque fichier l1x, l2x créer 3 fichiers distincts :

- l'un concernant les règles du gascon
- l'un concernant les règles du lengadocian
- le dernier concernant les règles communes

puis dans chaque mode on appelle le fichier de la variété suivit du fichier commun

mettre à jour le Makefile.am

mettre à jour les modes

### files

- [x] apertium-oci-fra.fra-oci.l1x
- [x] apertium-oci-fra.fra-oci.l2x
- [x] apertium-oci-fra.oci-fra.l1x
- [x] apertium-oci-fra.oci-fra.l2x

# modifications sur le contenu des fichiers

## dictionaire

ajouter les symboles pour les dialectes :

```xml
<sdef n="d:gascon" c="mot del dialècte Gascon"/>
<sdef n="d:lengadocian" c="mot del dialècte Lengadocian"/>
```

ajouter les paradigmes de dialèctes :

```xml
<pardef n="d:gascon">
  <e r="LR"><p><l></l><r></r></p></e>
  <e r="RL"><p><l><s n="d:gascon"/></l><r></r></p></e>
</pardef>

<pardef n="d:lengadocian">
  <e r="LR"><p><l></l><r></r></p></e>
  <e r="RL"><p><l><s n="d:lengadocian"/></l><r></r></p></e>
</pardef>
```

remplacer les occurences de `v="oci"`, `v="oci@gascon"` (`v="oci@aran` ?) par les paradigmes associés

## règles de sélection lexicale

~~voir [ici](./reglas-de-seleccion-lexicala.md)~~

pour chaque fichier lrx créer 4 fichiers distincts :

- l'un concernant les règles du gascon
- l'un concernant les règles du lengadocian
- l'un concernant les règles de l'aranes
- le dernier concernant les règles communes

puis dans chaque mode on appelle le fichier commun SUIVIT du fichier de la variété

mettre à jour le Makefile.am

mettre à jour les modes

- [x] apertium-oci-fra.fra-oci.n_a_adv.lrx
- [x] apertium-oci-fra.fra-oci.np.lrx
- [x] apertium-oci-fra.fra-oci.other.lrx
- [x] apertium-oci-fra.fra-oci.v.lrx
- [ ] apertium-oci-fra.oci-fra.n_a_adv.lrx
- [ ] apertium-oci-fra.oci-fra.np.lrx
- [ ] apertium-oci-fra.oci-fra.other.lrx
- [ ] apertium-oci-fra.oci-fra.v.lrx
