---
layout: post
title:  "Exploration des données pour les expG"
date:   2017-11-24 19:50:28
---

Cette série d'articles va nous amener à construire un modèle pour calculer les
**expected goals**. Je ne vais pas revenir ici sur la signification des expected goals, [plusieurs](http://www.10contre11.fr/2015/07/26/expected-goals/) [articles](http://www.cahiersdufootball.net/article-les-expected-goals-au-c%C5%93ur-de-la-revolution-statistique-5744) [expliquent](http://www.goal.com/fr/news/mais-que-sont-les-expected-goals-xg-la-statistique-du-moment/h9xobvstqhc0191f4nsdvs0q0) [très bien le sujet](http://www.goal.com/fr/news/mais-que-sont-les-expected-goals-xg-la-statistique-du-moment/h9xobvstqhc0191f4nsdvs0q0), en français ou [en anglais](http://www.bbc.com/sport/football/41822455).

Dans la suite de l'article, l'expression *expected goals* pourra être abbrégée **expG** ou **xG**.

## Les données

L'élément de base pour notre modèle est le jeu de données. Nous utiliserons ici des données issues du fournisseur [Opta](http://optasports.fr), obtenues depuis plusieurs sites dont [whoscored](https://www.whoscored.com/) et [squawka](http://www.squawka.com).

*Opta* fournit pour chaque match les données des évènements du match: passes, tirs, corners, etc. Les évènements étant horodatés, il est possible de reconstituer le film du match.

Dans cet article, nous allons analyser l'évènement de tir. Avec nos données horodatées, nous sommes en mesure de déterminer si un tir suit un corner, un centre, une passe en profondeur, etc.

Le jeu de données utilisé concerne les championnats de France, Italie, Espagne, Allemagne et Angleterre, ainsi que la Ligue Europa et la Ligue des Champions.

Au total, **178 427 tirs** sont analysés pour la période allant de la saison 2012/2013 à 2017/2018 (au 24/11/2017). Les buts contre son camp et les penalties ne sont pas inclus dans le jeu de données.

## Exploration générale

Commençons à explorer les données brutes telles qu'elles sont obtenues. Tout d'abord, voici la répartition des conséquences d'un tir tenté (bloqué par un défenseur, but, non-cadré, sauvé par le gardien, poteau).
Sur nos 178 427 tirs, 17 448 ont été marqués, soit 9.78% de taux de réussite. Les tirs sont majoritairement non-cadrés à 40% (71000 tirs), presqu'autant de tirs bloqués et arrêtés par le gardien à environ 24%, et 2% de tirs sur les montants.

![Résultats des tirs](/img/posts/20171124_exploration_donnees_pour_expg/resultats_tirs.png)

A l'aide des coordonnées de tir, nous pouvons calculer la distance de chaque tir par rapport au centre du but adverse.

Sur ce graphique, les barres bleues montrent le nombre de tir, les barres rouges le nombre de buts. Sans surprise, beaucoup de tirs sont pris depuis l'intérieur de la surface de réparation, à moins de 18 mètres.

![Distance des tirs](/img/posts/20171124_exploration_donnees_pour_expg/distance_tir.png)

Les coordonées permettent également d'obtenir l'angle de tir par rapport au centre du but adverse. Les tirs avec le plus grand angle sont privilégiés, et les buts suivent majoritairement la courbe du nombre de tirs tentés. Les angles à droite et à gauche du but sont cumulés pour obtenir le nombre de tirs et de buts. Pour l'angle de 90 degrés, seuls les tirs en face du but sont comptés donc le nombre de tirs chute.

![Angle des tirs](/img/posts/20171124_exploration_donnees_pour_expg/angle_tir.png)

## Ajout de données

Les données brutes ne permettent pas d'obtenir une description précise des tirs. L'horodatage des données permet de reconstituer l'action amenant au tir. Voici une analyse des actions précédant les tirs (dans l'ordre sur corner, centre, centre en retrait, passe d'un co-équipier, passe d'un adversaire, passe en retrait).

![Action avant tirs](/img/posts/20171124_exploration_donnees_pour_expg/action_avant_tir_passe.png)
