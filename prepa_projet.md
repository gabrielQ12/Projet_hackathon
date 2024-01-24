

## User story

3 profils : demandeur d'emploi - Recruteurs tech & RH - France Travail 

En tant que          | Je veux pouvoir                          | Afin de                                    
visiteur             |  créer un profil                         | avoir un profil                            
visiteur             |  voir les annonces                       | decider s'il sera interessant de créer un compte                   
visiteur             |  ce loguer                               | etre identifier                  
demandeur d'emploi   |  consulter les annonces                  | chercher un emploi                         
recruteur            |  créer un profil entreprise              | s'identifier 
recruteur            |  création d'arbre de compétance          | evaluer les dev
recruteur            |  modifier l'arbre de compétance          | faire evoluer  la demande 
recruteur            |  rediger une annonce                     | chercher un dev                            
recruteur            |  consulter les profils des dev           | voir le profil des dev qui font les tess des arbres
France travail       |  consulter les profils des dev           | proposer des candidats au entreprises        
France travail       |  création d'arbre de compétance          | evaluer les dev

-----

## [PROBABLEMENT INUTILE]                                                            

## visiteur           |  voir les profil public               | acceder au pages public 
## demandeur d'emploi |  modifier son profil                  | renseigner ses evolutions               
## demandeur d'emploi |  postuler à une annonce               | montrer mon interet en postulant         
## demandeur d'emploi |  remplir l'arbre de compétence        | montrer mes capacitées                 
## demandeur d'emploi |  voir les offres auquel il a postulé  | organiser ses candidatures 
## recruteur          |  consulter les profils public des dev | faire une première selection               
## recruteur          |  lire les résultats des tests         | voir les stack technique des dev            
## recruteur          |  contacter les dev                    | planifier un entretien                      
## recruteur          |  consulter les profils privé          | voir le cadidat
## demandeur d'emploi |  voir les profils public                 | voir l'etat du marché de l'emploi



## CRUD

|URL            | Requetes   | Description                                    | Données attendues 
signUP/         |    POST    | création d'un compte utilisateur ou entreprise | nom / prenom / MDP /  mail / genre / liens vers les divers sites
signIN/         |    POST    | acceder a son compte                           | nom / mdp
skiltrea/create |    POST    | créer un arbre de compétances a tester         | compétances / dificulté / temps / info / validation 
job/create      |    POST    | créer une annonce                              | info post / salaire / type de contrat / info Entreprise
jobs/all        |    GET     | récupérer les annonces                         | toutes les annonces
job/$#          |    GET     | récupérer une annonce                          | une annonce 
profil/$#       |    GET     | récupérer le profil d'un cadidat               | un profil complet 
skilltrea/update|   PATCH    | modifier l'arbre de compétences                | un arbre de compétances







## MCD
Voir schema brouillon_mcd


## MLD

Entité USER:
        id, nom, prenom, role, mdp,  mail

Entité CANDIDAT herite de USER:
        id as USER, presentation, lien github, lien linkedin, lien portfolio, lien dailyDev, lien autre, arbre réussi

Entité ENTREPRISE herite de USER:
        id as USER, nom de l'entreprise

Entité FRANCE TRAVAIL herite de USER:
        id as USER, 

Entité ARBRE:
        id, #TACHE_id,  place de la tache;  #USER_ID

Entité TACHE:
        id, #ARBRE_id, dificulté, temps, nom, description, test unitaire reussi, id tache parente

Enum ROLE : 
        CANDIDAT, ENTREPRISE, FRANCE TRAVAIL

## Dictionnaire de données

Table USER : 

| Champ           | Type       | Spécificités                                   | Description                             |
|-----------------|------------|------------------------------------------------|-----------------------------------------|


Table CANDIDAT : 

| Champ           | Type       | Spécificités                                   | Description                             |
|-----------------|------------|------------------------------------------------|-----------------------------------------|


Table ENTREPRISE 

| Champ           | Type       | Spécificités                                   | Description                             |
|-----------------|------------|------------------------------------------------|-----------------------------------------|


Table FRANCE TRAVAIL :

| Champ           | Type       | Spécificités                                   | Description                             |
|-----------------|------------|------------------------------------------------|-----------------------------------------|


Table ARBRE : 

| Champ           | Type       | Spécificités                                   | Description                             |
|-----------------|------------|------------------------------------------------|-----------------------------------------|


Table TACHE : 

| Champ           | Type       | Spécificités                                   | Description                             |
|-----------------|------------|------------------------------------------------|-----------------------------------------|


Table ROLE : 

| Champ           | Type       | Spécificités                                   | Description                             |
|-----------------|------------|------------------------------------------------|-----------------------------------------|


## Notes et idées

- lib JOI avec regex pour controler les données d'entré coté back
- lib Bcrypt pour le hash de MDP 
- JWT sur les routes concerné
- DOMpurify pour cleaner les entrant coté front
- pensé au CORS policy et autre failles Web basique 
- throw ERROR ==> modul de gestion d'erreurs ? 