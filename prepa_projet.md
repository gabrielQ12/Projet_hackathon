

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
skilltree/create|    POST    | créer un arbre de compétances a tester         | compétances / dificulté / temps / info / validation 
job/create      |    POST    | créer une annonce                              | info post / salaire / type de contrat / info Entreprise
jobs/all        |    GET     | récupérer les annonces                         | toutes les annonces
job/$#          |    GET     | récupérer une annonce                          | une annonce 
profile/$#      |    GET     | récupérer le profil d'un cadidat               | un profil complet 
skilltree/update|   PATCH    | modifier l'arbre de compétences                | un arbre de compétances


## MCD
Voir schema brouillon_mcd


## MLD

Entité USER:
        id, nom, prenom, role, mdp,  mail

Entité CANDIDAT herite de USER:
        id as USER, presentation, lien github, lien linkedin, lien portfolio, lien dailyDev, lien autre, #ARBRE_id,

Entité recruiter herite de USER:
        id as USER, nom de l'entreprise

Entité FRANCE TRAVAIL herite de USER:
        id as USER, 

Entité ARBRE:
        id, #TACHE_id,  place de la tache;  #USER_ID

Entité TACHE:
        id, #ARBRE_id, dificulté, temps, nom, description, test unitaire reussi, id tache parente

Enum : 
        CANDIDAT, ENTREPRISE, FRANCE TRAVAIL

## Dictionnaire de données

Table USER : 

| Champ           | Type       | Spécificités                                   | Description                              |
|-----------------|------------|------------------------------------------------|------------------------------------------|
|  ID             | INTEGER    | INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY   | Identification unique généré auto en BDD |
|  name           | TEXT       | NOT NULL                                       | Nom de l'utilisateur                     |
|  prenom         | TEXT       | NOT NULL                                       | Prenom de l'utilisateur                  |
|  Role           | ENUM       |                                                | Role de l'utilisateur                    |
|  MotDePasse     | VARCHAR(60)| NOT NULL UNIQUE                                | Mot de passe Hashé                       |
|  mail           | TEXT       | NOT NULL UNIQUE                                | Adresse mail de l'utilisateur            |

----------------

Table CANDIDAT : 

| Champ           | Type        | Spécificités                                   | Description                             |
|-----------------|-------------|------------------------------------------------|-----------------------------------------|
|  ID             | INTEGER     | INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY   | Identification unique généré auto en BDD|
|  ID_USER        | INTEGER     | INT REFERENCES user (id)                       | Clé étrangère fais référence a USER     |
|  Presentation   | TEXT        | NOT NULL                                       | Presentation du candidat                |
|  LienGithub     | TEXT        |                                                | Lien vers le profil github              |
|  LienLinkedIN   | TEXT        |                                                | Lien vers le profil LinkedIN            | 
|  LienPortfolio  | TEXT        |                                                | Lien vers le profil Portfolio           | 
|  LienDailyDev   | TEXT        |                                                | Lien vers le profil DailyDev            | 
|  LienAutre      | TEXT        |                                                | Lien libre                              | 
|  ID_Arbre       | INTEGER     | INT REFERENCES arbres (id)                     | Clé étrangère fais référence a ARBRE    |

----------------

Table ENTREPRISE 

| Champ           | Type       | Spécificités                                   | Description                             |
|-----------------|------------|------------------------------------------------|-----------------------------------------|
|  ID             | INTEGER    | INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY   | Identification unique généré auto en BDD|
|  nomEntreprise  | TEXT       | NOT NULL UNIQUE                                | Nom de l'entreprise                     |
|  ID_USER        | INTEGER    | INT REFERENCES user (id)                       | ID hérité de USER                       | 

----------------

Table FRANCE TRAVAIL :

| Champ           | Type       | Spécificités                                   | Description                             |
|-----------------|------------|------------------------------------------------|-----------------------------------------|
|  ID             | INTEGER     | INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY   | Identification unique généré auto en BDD|
|  ID_USER        | INTEGER     | INT REFERENCES user (id)                       | Clé étrangère fais référence a USER     |

----------------

Table ARBRE : 

| Champ           | Type       | Spécificités                                   | Description                             |
|-----------------|------------|------------------------------------------------|-----------------------------------------|
|  ID             | INTEGER    | INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY   | Identification unique généré auto en BDD|
|  ID_TACHE       | INTEGER    | INT REFERENCES tache (id)                      | ID hérité de TACHE                      |
|  placeDeLaTache | INTEGER    | INT NOT NULL                                   | Localisation de la tache au seins d'un arbre|
|  ID_USER        | INTEGER    | INT REFERENCES user (id)                       | Clé étrangère fais référence a USER     |

----------------

Table TACHE : 

| Champ           | Type       | Spécificités                                   | Description                             |
|-----------------|------------|------------------------------------------------|-----------------------------------------|
|  ID             | INTEGER    | INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY   | Identification unique généré auto en BDD|
|  ID_Arbre       | INTEGER    | INT REFERENCES arbres (id)                     | Clé étrangère fais référence a ARBRE    |
|  Dificulté      | INTEGER    | INT NOT NULL                                   | Niveau de dificulté de la tache         |
|  Temps          | ITIMESTAMP | UNIQUE                                         | Durée de la tache                       |
|  name           | TEXT       | NOT NULL                                       | Nom de la tache                         |
|  Description    | TEXT       | NOT NULL                                       | Description de la tache                 |
|  TestOk         | BOOL       | DEFAULT false                                  | Check pour savoir si le test unitaire prévu est réussi |
## |  IDTacheParente | INTEGER    |  ?? Je ne sais aps si c'est une clé étrangère ou juste une valeur qui fais référence a l'ID

----------------



## Notes et idées

- lib JOI avec regex pour controler les données d'entré coté back
- lib Bcrypt pour le hash de MDP 
- JWT sur les routes concerné
- DOMpurify pour cleaner les entrant coté front
- pensé au CORS policy et autre failles Web basique 
- throw ERROR ==> modul de gestion d'erreurs ? 