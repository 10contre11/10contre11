---
layout: post
title:  "Classement ELO"
date:   2015-09-25 21:59:08
---

<style>
  table {
    border-spacing: 0;
    border-collapse: collapse;
  }

  table th {
    padding: 4px;
    border-top: 1px solid #CCC;
    border-bottom: 2px solid #000;
    text-transform: uppercase;
    text-align: left;
  }

  table td {
    padding: 4px 8px;
    border-bottom: 1px solid #CCC;
    font-size: 15px;
  }
</style>

<script type="text/javascript" src="/js/posts/2015-09-25-classement-elo.js"></script>

<script type="text/javascript"
  src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
</script>

<script type="text/javascript">
    MathJax.Hub.Config({
      "HTML-CSS": {
        preferredFont: "STIX"
      }
    });
</script>

La comparaison de deux équipes de football n'est pas toujours chose aisée. Le premier moyen utilisé est
souvent la place au classement du championnat. On utilise parfois également le nombre de buts marqués ou
encaissés. La comparaison des joueurs composant les équipes peut également servir de base.

Si le championnat n'est pas assez avancé et que les équipes ne se sont pas toutes rencontrées, le classement
par point ou le nombre de buts marqués ou encaissés ne permettent pas de comparer objectivement deux équipes.
Le **classement Elo**, utilisé initialement pour classer les joueurs d'échec, est un outil plus sûr pour comparer
la valeur des équipes.

## Aux origines

En 1960, la fédération américaine d'échec adopte le classement Elo pour classer ses joueurs. Ce système inventé
par **Arpad Elo** permet de classer les joueurs en ajoutant ou retirant après chaque match un nombre de points,
calculés en fonction du niveau de leurs adversaires.

Chaque joueur possède un nombre de points en fonction de ses performances passées. Plus le nombre de points est
élevé, plus le joueur est performant. Lors des confrontations entre joueurs, si un joueur obtient des performances
supérieures à son niveau estimé, il gagne des points Elo, et inversement en cas de contre-performances.

## Fonctionnement

Adapté au football, lorsque deux équipe se rencontrent, une probabilité de gain est calculée à partir du classement de chaque équipe.
La formule suivante détermine cette probabilité de gain:

<math display='block'>
    <mrow>
        <msub>
            <mi>p</mi>
        </msub>
        <mo>=</mo>
        <mfrac>
            <mrow>
                <msub>
                    <mi>1</mi>
                </msub>
            </mrow>
            <mrow>
                <msub>
                    <mi>1</mi>
                </msub>
                <mo>+</mo>
                <msup>
                    <mi>10</mi>
                    <mn>-dr/400</mn>
                </msup>
            </mrow>
        </mfrac>
    </mrow>
</math>

Où *dr* est la différence de points Elo entre les deux équipes. A partir de cette probabilité, le nombre de points Elo
gagnés ou perdus sont calculés par la formule suivante:

<math display='block'>
    <mrow>
        <msub>
            <mi>&Delta;Elo</mi>
        </msub>
        <mo>=</mo>
        <mrow>
          <mi>(R - p)</mi>
          <mo>*</mo>
          <mi>k</mi>
        </mrow>
    </mrow>
</math>

Où *R* est le résultat de l'équipe (1 pour une victoire, 0.5 pour un nul et 0 pour une défaite), *p* est la probabilité de
victoire calculée précédement et *k* est le coefficient de développement. Pour le classement Elo aux échec, ce coefficient
doit permettre aux nouveaux joueurs d'atteindre rapidement leur niveau réel, il varie donc comme ceci:

 * **40** pour les 30 premières parties
 * **20** tant que le joueur est sous les 2400 points
 * **10** au dessus de 2400 points

Un coefficient élevé permet d'atteindre rapidement la valeur réelle mais subit de nombreuse variations, tandis qu'un
coefficient plus faible converge moins rapidement vers le niveau réel mais est plus stable.

Pour les clubs de football, un classement Elo est déterminé par le site [clubelo.com](http://www.clubelo.com "clubelo.com").
Ce site utilise le coefficient **k = 20**, valeur qui sera le notre puisque les valeurs de ce site seront utilisées dnas les
exemples suivants.

## Exemple d'échange de points

Un exemple sera sûrement plus parlant que la théorie. Prenons le cas du match **Marseille - Angers** disputé le 27 septembre 2015.
Avant ce match, selon le site [clubelo.com](http://www.clubelo.com "clubelo.com"), Marseille a un classement Elo de **1686**, tandis qu'Angers est à **1526**. L'écart au
classement Elo entre les deux équipes est donc de 160 en faveur de Marseille.

Pour commencer, calculons la probabilité de gain pour **Marseille**:

<math display='block'>
    <mrow>
        <msub>
            <mi>p</mi>
        </msub>
        <mo>=</mo>
        <mfrac>
            <mrow>
                <msub>
                    <mi>1</mi>
                </msub>
            </mrow>
            <mrow>
                <msub>
                    <mi>1</mi>
                </msub>
                <mo>+</mo>
                <msup>
                    <mi>10</mi>
                    <mn>-160/400</mn>
                </msup>
            </mrow>
        </mfrac>
        <mo>=</mo>
        <mi>0.715</mi>
    </mrow>
</math>

Pour **Angers**, la probabilité est logiquement inverse, soit:

<math display='block'>
    <mrow>
        <msub>
            <mi>p</mi>
        </msub>
        <mo>=</mo>
        <mfrac>
            <mrow>
                <msub>
                    <mi>1</mi>
                </msub>
            </mrow>
            <mrow>
                <msub>
                    <mi>1</mi>
                </msub>
                <mo>+</mo>
                <msup>
                    <mi>10</mi>
                    <mn>160/400</mn>
                </msup>
            </mrow>
        </mfrac>
        <mo>=</mo>
        <mi>0.285</mi>
    </mrow>
</math>

A partir de ces valeurs, nous pouvons déterminer le gain de points Elo pour Marseille en cas de victoire:

<math display='block'>
    <mrow>
        <msub>
            <mi>&Delta;Elo</mi>
        </msub>
        <mo>=</mo>
        <mrow>
          <mi>(1 - 0.715)</mi>
          <mo>*</mo>
          <mi>20</mi>
        </mrow>
        <mo>=</mo>
        <mi>5.7</mi>
    </mrow>
</math>

Dans ce cas, Angers perdrait le nombre de points suivants:

<math display='block'>
    <mrow>
        <msub>
            <mi>&Delta;Elo</mi>
        </msub>
        <mo>=</mo>
        <mrow>
          <mi>(0 - 0.285)</mi>
          <mo>*</mo>
          <mi>20</mi>
        </mrow>
        <mo>=</mo>
        <mi>-5.7</mi>
    </mrow>
</math>

On constate que le nombre de points gagnés ou perdu est identique. En fait, le classement Elo est établi par un
**transfert de points** d'une équipe vers une autre, ici *5.7* points en cas de victoire de l'OM.

En cas de victoire angevine en terre phocéenne, Angers gagnerait *14.3* points que l'OM perdrait.

Enfin, en cas de match nul, Marseille perdrait *4.3* points récupérés par Angers. Cet exemple illustre bien le gain
de points en fonction de la **valeur de chaque équipe** avant le match. Un résultat logique provoque un **faible échange** de points,
tandis qu'une contre-performance implique un échange d'un nombre plus **important de points**.

## Classement Elo en Ligue 1

Voici le classement Elo en Ligue 1 au 25 septembre 2015, avec dans la dernière colonne la différence entre le nombre de points
au 25/09/2015 et le nombre de points avant le début de la saison 2015/2016 de Ligue 1:

<div id="elo_ligue1"></div>

On constate de façon marquante la sous-performance de Montpellier et de Monaco, ainsi que Troyes qui avait 1563 points Elo
au début du championnat.

Rennes, Reims et Angers sont les équipes ayant le plus progressé depuis le début de la saison.

## Plus gros exploits en Ligue 1

Avec le classement Elo, nous pouvons déterminer les plus gros exploits en terme de résultat par rapport à la force présumée
de chaque équipe. Voici les **15 plus gros exploits** en Ligue 1 entre les saisons 2012/2013 et 2014/2015:

<div id="elo_ligue1_upsets"></div>

On retrouve évidemment les quelques contre performances de l'équipe phare des ces dernière saisons en Ligue 1, le **PSG**. Il est
plus "simple" de réaliser un exploit à domicile, **Lyon** est la seule équipe qui déroge à la règle avec deux défaites à domicile
en tant que grand favoris.

Le classement Elo est un outil très intéressant pour évaluer le niveau relatif des équipes. Nous verrons dans un prochain article
comment utiliser ce classement pour aller plus loin dans la comparaison des équipes.

<script type="text/javascript">
  elo_ligue1("#elo_ligue1");
  elo_ligue1_upsets("#elo_ligue1_upsets");
</script>
