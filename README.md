# "Hello world" TexInfo

- ["Hello world" TexInfo](#hello-world-texinfo)
  - [TexInfo](#texinfo)
  - [Installer](#installer)
  - [Créer un fichier TexInfo](#créer-un-fichier-texinfo)
  - [Compiler](#compiler)
  - [Références](#références)


## TexInfo

[TexInfo](https://fr.wikipedia.org/wiki/Texinfo) a pour but de fournir une façon simple de créer de la documentation logicielle. C'est un langage de formatage de texte (markup), conçu par Richard Stallman. 

C'est une surcouche à [Tex](https://fr.wikipedia.org/wiki/TeX), spécifiquement conçue pour la documentation technique, permettant la génération de documents qui peuvent être exportés dans plusieurs formats (PDF, DVI, HTML, Docbook, Info, etc.). *Une source, plusieurs publications*. 

C'est le langage de documentation officielle du [projet GNU](https://fr.wikipedia.org/wiki/Projet_GNU).

## Installer

[Télécharger la dernière version de `texinfo`](https://ftp.gnu.org/gnu/texinfo/) et compiler en suivant les instructions des `INSTALL` et `INSTALL.generic`. 

Pensez à télécharger aussi le fichier [`texinfo.tex`](https://ftpmirror.gnu.org/gnu/texinfo/texinfo.tex).

## Créer un fichier TexInfo

Créer un fichier `hello.texi` avec le contenu suivant (issu du manuel) :

~~~tex
\input texinfo
@settitle Sample Manual 1.0

@copying
This is a short example of a complete Texinfo file.

Copyright @copyright{} 2016 Free Software Foundation, Inc.
@end copying

@titlepage
@title Sample Title
@page
@vskip 0pt plus 1filll
@insertcopying
@end titlepage

@contents

@node Top
@top GNU Sample

This manual is for GNU Sample
(version @value{VERSION}, @value{UPDATED}).

@menu
* First Chapter::    The first chapter is the
                      only chapter in this sample.
* Index::            Complete index.
@end menu


@node First Chapter
@chapter First Chapter

@cindex chapter, first
This is the first chapter.
@cindex index entry, another

Here is a numbered list.

@enumerate
@item
This is the first item.

@item
This is the second item.
@end enumerate



@node First Section
@section First Section

First section of first chapter.


@node Second Section
@section Second Section

Second section of first chapter.


@node Index
@unnumbered Index

@printindex cp

@bye
~~~


## Compiler

Placer le fichier `texinfo.tex` à la racine du projet. Puis :

~~~bash
#produire un fichier dvi (pour impression)
texi2dvi hello.texi
#produire un fichier pdf
texi2dvi --dvipdf hello.texi
#produire un site web
texi2any --html hello.texi
#produire un fichier standalone .info, lisible par le reader info
makeinfo hello.texi
#makeinfo est un alias de texi2any. Idem que précédent :
texi2any hello.texi
#Lire le fichier .info avec le reader de GNU
#Le reader est puissant et offre de nombreuses possibilités
#de navigation et de recherche (inspiré/basé sur Emacs)
info hello.info
#Doc
man texi2dvi
man makeinfo
~~~

Lors de la phase de compilation, le fichier source `.texi` inclut le fichier `texinfo.tex` qui contient les commandes nécessaires à l'interprétation des commandes TexInfo (@-commandes) en commandes/macros TeX. Ce fichier définit également la mise en page, la typographie et le style du document produit. **Il est indispensable : c'est la surcouche de TeX sur laquelle est bâtie TexInfo**.

> `texi2dvi` est un script bash qui appelle `tex` et `dvips` pour produire un document imprimable bien formé (l'index, etc.). Consulter le début du fichier `texinfo.tex` pour plus d'information.


## Références

- [Page web du projet TexInfo](https://www.gnu.org/software/texinfo/), sur le site officiel [gnu.org](https://www.gnu.org/)
- [Le manuel de TexInfo](https://www.gnu.org/software/texinfo/manual/texinfo/texinfo.html#SEC_Contents), rédigé et publié avec TexInfo évidemment. Apprendre à vous servir de TexInfo pour rédiger de la documentation technique
- [Télécharger la dernière version de `texinfo` (programmes, fichiers) (serveur ftp)](https://ftp.gnu.org/gnu/texinfo/), télécharger les sources et compiler en suivant les instructions contenus dans `INSTALL` et `INSTALL.generic`;
- [Télécharger la dernière version du fichier `texinfo.tex`](https://ftpmirror.gnu.org/gnu/texinfo/texinfo.tex), **indispensable**