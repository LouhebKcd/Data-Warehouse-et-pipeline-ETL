# Ontologie des véhicules

Ce fichier présente nos réalisations dans le cadre du projet d’ontologie des véhicules.

L’objectif du projet est de modéliser, en OWL, un domaine riche autour des véhicules (légers et lourds) et des entreprises qui les exploitent, afin de pouvoir interroger ces connaissances via des requêtes DL Query et SPARQL.

---

## Contenu du dépôt

- `vehicule.owl` : fichier OWL contenant l’ontologie des véhicules.
- `query.txt` : fichier listant les requêtes DL Query et SPARQL ainsi que les résultats obtenus.
- `compte_rendu.pdf` : compte-rendu détaillé du projet (modélisation, choix et exemples de requêtes).

---

## Modélisation de l’ontologie

### Classes principales

L’ontologie est structurée autour de plusieurs concepts clés :

- `VehiculeLeger`
- `VehiculeLourd`
- `Entreprise`
- Classes associées aux chantiers, chauffeurs, usages (transport de marchandises, levage, transport de personnes, etc.), types de moteurs et transmissions.

Cette structuration permet de couvrir aussi bien les véhicules légers (transport de personnes) que les véhicules lourds (chantier, transport de marchandises, agriculture, etc.).

### Propriétés d’objet

Nous avons défini différentes relations entre les concepts, notamment :

- `appartientALentreprise` : relie un véhicule à l’entreprise qui le possède.
- `aPourConstructeur` : relie un véhicule à son constructeur (Renault, Volvo, Peugeot, etc.).
- `aPourChauffeur` : association entre un véhicule et son chauffeur.
- `travailleSurChantier` : lien entre les matériels et les chantiers sur lesquels ils interviennent.
- `estUtiliséPour` : décrit l’usage prévu (transport de marchandises, levage, excavation, transport de personnes…).

### Propriétés de données

Chaque véhicule est décrit par des attributs, par exemple :

- type de moteur / énergie (essence, diesel, électrique, hybride, …),
- capacité de charge en tonnes pour les véhicules lourds,
- consommation moyenne en L/100 km pour certains véhicules légers,
- autres caractéristiques techniques (transmission manuelle, automatique, etc.).

---

## Individus

Pour illustrer des scénarios réalistes, l’ontologie contient des individus représentant :

- **Véhicules lourds** : `Renault_Kerax`, `Renault_Premium`, `DAF_XG`, `Mercedes_Actros`, `Scania_Serie_L`, `Volvo_FH`, `Pelleteuse_Hyundai_250`, `Mini_Pelle_Takeuchi_5.7T`, `Grue_Mobile_Liebher`, etc.
- **Véhicules légers** : `Peugeot_406`, `Peugeot_308`, `Renault_Clio`, `Toyota_Hilux`, `Ford_Raptor`, `Yamaha_TMAX`, `Harley_Davidson_Fat_Bob`, etc.
- **Entreprises** : `ETS_KACED`, `SARL_Djeha`.
- **Chantiers** et **chauffeurs** : utilisés pour relier les matériels aux chantiers et aux conducteurs.

Ces individus permettent de tester l’ontologie sur des cas d’usage concrets de gestion de flotte et d’affectation sur chantiers.

---

## Requêtes DL (DL Query)

Nous avons formulé plusieurs requêtes DL pour interroger l’ontologie, par exemple :

1. **Camions Renault avec capacité > 20 tonnes**  
   - Objectif : retrouver les camions construits par Renault ayant une capacité de charge supérieure à 20 tonnes.
   - Résultat : `Renault_Kerax`, `Renault_Premium`.

2. **Camions de SARL_Djeha pour le transport de marchandises, capacité > 10 tonnes**  
   - Objectif : identifier les véhicules lourds appartenant à `SARL_Djeha`, utilisés pour le transport de marchandises, avec une capacité supérieure à 10 tonnes.

3. **Véhicules légers Peugeot, Diesel, transmission manuelle, transport de personnes**  
   - Objectif : retrouver les véhicules légers construits par Peugeot, équipés d’un moteur Diesel, d’une transmission manuelle, utilisés pour le transport de personnes.

Toutes les requêtes DL et les résultats associés sont détaillés dans le fichier `query.txt`.

---

## Requêtes SPARQL

Nous avons également mis en place des requêtes SPARQL pour extraire des vues plus riches :

1. **Matériels d’ETS_KACED, chantiers et chauffeurs associés**  
   - Liste, pour l’entreprise `ETS_KACED`, de chaque matériel avec le chantier sur lequel il travaille et le chauffeur associé.

2. **Matériels lourds par entreprise**  
   - Pour chaque entreprise : liste des véhicules lourds avec le constructeur, l’usage, le type de moteur et la capacité de charge (en tonnes).

3. **Véhicules légers par constructeur et caractéristiques**  
   - Pour chaque constructeur : liste de ses véhicules légers, avec moteur, transmission et consommation moyenne.

Ces requêtes, ainsi que leurs résultats, sont également présentes dans `query.txt`.

---

## Outils utilisés

- **Protégé** pour la conception et l’édition de l’ontologie OWL.
- Un raisonneur (HermiT, Pellet, …) pour vérifier la cohérence de l’ontologie et exécuter les DL Queries.
- L’onglet **SPARQL** de Protégé pour les requêtes SPARQL.

---

## Comment tester le projet

1. Ouvrir `vehicule.owl` dans **Protégé**.
2. Activer le raisonneur (par ex. HermiT).
3. Dans l’onglet **DL Query**, saisir les requêtes présentes dans `query.txt` et vérifier que les résultats correspondent à ceux indiqués.
4. Dans l’onglet **SPARQL**, copier-coller les requêtes depuis `query.txt` et exécuter pour retrouver les mêmes tableaux de résultats.

---

## Améliorations possibles

- Ajouter de nouvelles classes (ex : contrats de location, opérations de maintenance, types de remorques, etc.).
- Raffiner les contraintes (cardinalités, restrictions sur les propriétés) pour exprimer plus précisément les règles métier.
- Aligner l’ontologie avec des vocabulaires externes (ontologies de transport existantes, standards du web sémantique).
