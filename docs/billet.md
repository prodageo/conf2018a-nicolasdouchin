# Avec les GitLab Runners, comme Mickey dans Fantasia, devenez un apprenti sorcier de l'intégration continue (et du déploiement) 

## Cartouche d'identification

 - Manifestation : CodeursEnSeine 2018
 - Lieu : Kindarena Métropole Rouen Normandie
 - Conférence : Avec les GitLab Runners, comme Mickey dans Fantasia, devenez un apprenti sorcier de l'intégration continue (et du déploiement) 
 - Horaire de la conférence : 14h30
 - Durée de la conférence : 50 minutes
 - Conférencier(s) :
   - Philippe Charrière ([LinkedIn](https://www.linkedin.com/in/phcharriere/), [Github](https://github.com/k33g), [Twitter](https://twitter.com/k33g_org))
 - Audience : ~130
 - Mots-clés : Gitlab, Gitlab CI/CD, continuous integration & delivery, test automation
 - URL de l'illustration : ![Avec les GitLab Runners, comme Mickey dans Fantasia, devenez un apprenti sorcier de l'intégration continue (et du déploiement)](illustration.jpg)

## Support
 - Lien vers le support (diapos) présenté en conférence : indisponible
 - Nombre de diapos du support : N/A
 - Plan du support : 
   - Présentation de Gitlab et plus particulièrement de Gitlab CI/CD
   - Présentation du système de templates pour créer des dépôts facilement.
   - Explication du fichier `.gitlab-ci.yml`.
   - Lancement des tests sur différentes branches.
   - Exemple de livraison grâce à l'outil de déploiement.

## Résumé
Gitlab est une plateforme permettant de gérer le cycle de vie de son produit de A à Z. Allant du développement à la livraison en passant par les tests. Gitlab propose pour cela une fonctionnalité : Gitlab CI/CD (Continuous Integration/Continuous Delivery). Cet outil va pouvoir gérer les phases de tests, de build et de déploiement de notre application et ce la de manière automatisée.

Tout est défini dans un fichier `.gitlab-ci.yml` qui définit les différents jobs et les contraintes et règles (par exemple, le job "deploiement" ne se déclenchera que sur la branche master) appliquées aux jobs. Afin d'exécuter ces jobs, il faut installer un runner sur une machine. Le runner va avoir pour rôle de poll régulièrement gitlab afin de vérifier si des modifications ont été apportées au code sur les différentes branches. Il exécutera ensuite les différents scripts définis par les jobs décrits dans le fichier `.gitlab-ci.yml`. L'enchaînement de l'exécution des jobs est appelé "Pipeline". A chaque push, un pipeline sera créé. Il est possible de voir l'état de ceux-ci depuis l'interface WEB de gitlab qui va également afficher la console d'exécution du pipeline et ainsi permettra de voir où une erreur s'est produite. Il est également possible d'extraire des rapports/logs de ces pipelines en les plaçant dans des artefacts dont on peut définir une durée de vie.

La conférence est une démonstration de l'ensemble des fonctionnalités de Gitlab CI/CD (les demandes de fusion sont également montrées). On y voit donc l'application de toutes les étapes décrites plus haut. Vers la fin de la conférence, une démonstration du déploiement de l'application sur des plateformes externes comme [OpenFaaS](https://github.com/openfaas/faas) et [Clever Cloud](https://www.clever-cloud.com/fr/).

## Architecture et facteur qualité

Les facteurs qualités de l'ISO 9126:2001 concernant cette conférence et plus particulièrement Gitlab CI est la **Maintainability**. Ce facteur comprend plusieurs sous-facteurs :

* M1 Analyzability : grâce à son interface WEB permettant d'afficher l'état des Pipelines mais également de pouvoir accéder à des rapports (stockés en tant qu'artefacts) afin de pouvoir analyser ce qui s'est passé au niveau de l'application lors du passage dans la pipeline.
* M2 Changeability : c'est le principe même de Gitlab : permettre de réaliser des modifications de l'application. C'est la base du système et c'est sur cette base que viennent se greffer les différents services de Gitlab.
* M3 Stability : ce sous-facteur est assuré par le lancement d'une pipeline à chaque push. Si une pipeline ne passe pas les tests, la branche associée ne pourra pas être fusionnée et donc l'application finale ne pourra pas être mise à jour. Cela permet de maintenir la stabilité de l'application en production. Nous pouvons également associer la notion de Git Flow à ce sous-facteur.
* M4 Testability : c'est le principe même de Gitlab CI : permettre de lancer une baterie de tests. Ces tests permettront de valider les modifications réalisées, le résultat de ces tests seront disponibles au niveau du pipeline associé.
* M5 Maintainability Compliance : ce principe est lié au fichier `.gitlab-ci.yml` permettant de définir tout un ensemble de règle pour les tests, le build et le déploiement. Ces règles permettent de maintenir la conformité de la maintenabilité.

Enfin, il est possible d'associer le facteur **Portability** mais seulement pour quelques sous-facteurs. Ce facteur est plus lié à Gitlab CD.

* P2 Installability : le principe de la phase de déploiement est de pouvoir installer notre application dans un environnement précis. 
* P4 Replaceability : il est à la fois possible d'installer l'application dans un environnement défini à l'avance, mais également de remplacer l'ancienne version de l'application par la nouvelle venant d'être générée.
