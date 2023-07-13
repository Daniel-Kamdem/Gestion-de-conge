# Gestion congés

## Installation

Installer les dépendences:

### Client
- Node.js
- npm

### Serveur
- Java
- Maven

```
pushd client
npm install
popd
```


## Structure

La structure du projet est la suivante:

- server:

   Config : La configuration de Spring .
Controller : Un contrôleur est une classe Java portant l'annotation @Controller. L'objectif d'un contrôleur est de réagir à une interaction avec l'utilisateur, cela signifie que l'utilisateur envoie des requêtes HTTP au serveur. Elles sont traitées par les services, qui retournent les résultats sous forme de DTO.
DTO :  (Data Transfer Object, en anglais) est un patron de conception utilisé dans les architectures logicielles objets. Son but est de simplifier les transferts de données entre les sous-systèmes d'une application logicielle.
Entités ou Model : Une entité est une instance d'une classe qui sera persistante (que l'on pourra sauvegarder dans / charger depuis une base de données relationnelle). Une entité est signalée par l'annotation @Entity dans la classe. Elle appartient en général à un repository (une table de base de données). 
Enums : Ce sont les énumérations métier.
Repositories :  @Repository est une annotation Spring pour indiquer que l’interface a pour rôle de communiquer avec les tables de base de données, via JPA, donc ça contient optionnellement des méthodes de requête.
Services : Traite les requêtes venant du contrôleur, en s'aidant des repositories. C'est là que repose le cœur du métier. 
Security : Implémentation de l'authentification Spring via un Salarie. 
Helpers : Les helpers sont des classes outils qui contiennent du code susceptible d'être utilisable partout dans une application.

Guards : Gère qui peut accéder à certains chemins de l'application (si l'utilisateur est connecté ou a les droits pour) 
Localisation : Traduction du texte de l'application.
Model : Equivalent aux entités du côté serveur, c'est les objets métier.
Services : Gère la communication avec le serveur, effectue les requêtes pour obtenir et transmettre les informations (ça touche aux contrôleurs du serveur).
Site : Les pages et composants du site, en général ça injecte des services pour communiquer avec le serveur. Ces pages contiennent un module qui spécifie la route vers celle-ci, et un composant qui définit la logique (.TS) et le contenu de la page (.HTML/.CSS).
Shared : Les composants partagés entre les pages, y compris la barre de navigation et les validateurs de formulaire.

LES DIFFERENTES ANNOTATIONS :

Une annotation, c’est-à-dire @[nom de l’annotation], peut être ajoutée à une classe, une méthode, un attribut. L’annotation influe sur le comportement du programme car elle fournit des métadonnées lors de la compilation ; ces mêmes métadonnées seront utilisées lors de l’exécution.
@Inheritance La stratégie Table unique crée une table pour chaque hiérarchie de classe. JPA choisit également cette stratégie par défaut si nous n'en spécifions pas explicitement. Nous pouvons définir la stratégie que nous voulons utiliser en ajoutant cette annotation à la superclasse :
@Setter, @Getter @Accessor L'utilisation de ces annotations supprime le besoin d'implémenter manuellement les méthodes de mutation et d'accès. Bien que la plupart des IDE vous permettent de générer ces méthodes, l'utilisation de Lombok rend vos classes plus propres, en particulier lorsque vous avez une longue liste de champs. 
@NoArgsConstructor, @AllArgsConstructor
Cet ensemble de 2 annotations génère un constructeur qui acceptera 1 paramètre pour certains champs, et assigne simplement ce paramètre au champ.
@NoArgsConstructor générera un constructeur sans paramètres. Si cela n'est pas possible (à cause des champs finaux), une erreur de compilation se produira à la place, sauf si @NoArgsConstructor(force = true)est utilisé, alors tous les champs finaux sont initiali-sés avec 0/ false/ null. 
@Column Spécifie la colonne mappée pour une propriété ou un champ persistant. Si au-cune annotation de colonne n’est spécifiée, les noms de fichiers seront utilisés pour le mappage.  
@GeneratedValue
Cette annotation indique que la clé primaire est générée de façon automatique lors de l’insertion en base. Sans cette annotation, la valeur de l’identifiant de la clé primaire doit être affectée avant l’insertion en base.
Elle est utilisée avec une autre annotation @Id qui permet de mapper une clé primaire sur un champ unique.
Cette annotation possède plusieurs attributs : strategy, generator. Nous pouvons définir le mode de génération de la clé primaire à l’aide de l’attribut strategy.
Cet attribut peut prendre plusieurs valeurs :
Strategy = GenerationType.AUTO : La génération de la clé primaire est laissée à l’implémentation.  C’est hibernate qui s’en charge et qui crée une séquence unique sur tout le schéma via la table hibernate_sequence.
@Configuration cette annotation permet de déclarer pour Spring un composant qui ne sert qu'à configurer le contexte de l'application. Normalement ce composant n'est pas destiné à être injecté comme dépendance mais à déclarer des méthodes de fabrique an-notées avec @Bean.
@override est utilisé pour définir une méthode qui est héritée de la classe parente. On ne l'utilise donc que dans le cas de l'héritage.
@SpringBootTest est une annotation fournie par Spring Boot. Elle permet lors de l’exécution des tests d’initialiser le contexte Spring. Les beans de notre application peu-vent alors être utilisés.
@SpringBootApplication est un composé de 3 autres annotations :
1.	@SpringBootConfiguration : la classe sera utilisée comme une classe de configura-tion (on reviendra sur cette notion plus tard).
2.	@EnableAutoConfiguration : active la fameuse fonctionnalité d’autoconfiguration de Spring Boot, que je vous ai tant vantée.
3.	@ComponentScan : active le “scanning” de classes dans le package de la classe et dans ses sous-packages. Sans cette annotation, l’IoC container ne tiendra pas compte de vos classes, même si vous avez ajouté une annotation sur celles-ci. 

