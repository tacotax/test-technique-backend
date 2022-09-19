# Climb - Test technique Backend
## Sommaire
1. Objectif
2. Techno
3. Spécificités
4. Plus loin

## Objectif :
L'objectif est de créer un service permettant d'uploader un questionnaire et de récupérer les données liées à ce questionnaire au format JSON.
Ces données sont utilisées pour construire un questionnaire du type [suivant](https://www.weareclimb.fr/analyse-defiscalisation)
Les données du formulaire doivent être validées afin d'autoriser la sauvegarde.

Les tâches sont les suivantes :

* Page simple permettant d'uploader un fichier yaml. (Le fichier d'upload est au format yaml car je le trouve moins "verbeux" pour des profils non technique que le JSON)
* Vérification de la validité du questionnaire
* Endpoint permettant de récupérer les données sous format JSON à partir de la référence du questionnaire. Par exemple `GET localhost:3000/questionnaires/:reference` ou `:reference` est la référence du questionnaire uploadé.
* Ecrire un test sur les fonctionnalités implémentés
* L'exemple du questionnaire à uplaoder est le [suivant](https://github.com/tacotax/test-technique-backend/blob/master/questionnaire.yml)

## Techno :
Ruby on Rails, le choix de la base de données est libre.
Rspec pour les tests.

## Spécificités :
### Upload
* Page d'upload, `GET localhost:3000/questionnaires/new` avec la possibilité de choisir un fichier à uploader
* POST `localhost:3000/questionnaires` avec le fichier choisi
* Validation du questionnaire
* Si le questionnaire est valide alors redirection vers la page d'upload avec un message flash `L'upload du questionnaire a réussi`
* Si questionnaire non valide alors redirection vers la page d'upload avec un message affichant les références du questionnaire ayant posé problème

### Types d'éléments
* questionnaire :  
  élément racine, sa référence sera celle utilisée pour récupérer les données au format JSON via GET `localhost:3000/questionnaires/:reference`.  
  Valide la présence d'une référence et d'un contenu au moins.
* slide :  
  représente une des "page" du questionnaire  
  Valide la présence d'une référence, d'un label et d'un contenu au moins.
* text_input :  
  Valide la présence d'une référence, d'un label.
* number_input :  
  Valide la présence d'une référence, d'un label.
* boolean :  
  Valide la présence d'une référence, d'un label.
* single_choice :  
  Valide la présence d'une référence, d'un label, et d'au moins une réponse.  
  Un élément de réponse valide la présence d'un label et d'une value.
* multiple_choice :  
  Valide la présence d'une référence, d'un label, et d'au moins une réponse.  
  Un élément de réponse valide la présence d'un label et d'une value.

### Validation du questionnaire
* Le formulaire doit être au format YAML
* Chaque élément du questionnaire doit avoir un type
* Seul les types décrits plus haut sont autorisés
* Chaque élément valide à minima ce qui est décrit plus haut

### Plus loin
Pourront être discutés à posteriori par exemple :
* Les choix pris concernant la façon de stocker les données
* La mise en place d'une fonctionnalité de versionning sur les questionnaires
