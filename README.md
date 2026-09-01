# Inscryption

Cette application imite le jeu vidéo **Inscryption**.

## Installation

Après avoir copié le dépôt Git, assurez-vous d'utiliser la version **java 25 SDK** de Intellij Idea.

Certaines fonctionnalités risquent de ne pas marcher si nous n'utilisons pas cette version de l'IDE.

---

## Le jeu de cartes
### But du jeu 
Le joueur joue contre un adversaire
A la gauche du joueur, se trouve une balance symbolisant l'écart de score avec son adversaire. Le premier joueur qui atteint un écart de 5 points en sa faveur remporte la partie. 

### Emplacement des différents éléments de jeu
- Face à vous, se trouve un plateau constitué de deux lignes de quatre emplacements de cartes. Vous ne pouvez placer des cartes que sur la ligne du bas, votre adversaire uniquement sur la ligne du haut.
- A votre droite, vous disposez d'une pioche. Vous commencez avec 4 cartes en mains et vous pouvez piocher une carte par tour.

### Les cartes animaux
- Chaque carte dispose
  - d'un nombre de points d'attaque
  - d'un nombre de points de vie,
  - d'un nombre de vos cartes sur le plateau à sacrifier pour pouvoir être placée sur le plateau (nombre de gouttes de sang)
  - d'un nombre de vos cartes déjà mortes (tuées ou sacrifiées) pour pouvoir être placée sur le plateau (nombre d'os)

Chacune des cartes peut apparaitre en plusieurs exemplaires dans la pioche, dans la main et sur le plateau.

### Déroulement d'un tour
- Au début de votre tour, votre adversaire indique quelles cartes il jouera au tour prochain (représentés par une ligne supplémentaire de 4 emplacements de cartes au-dessus du plateau)
- A chaque tour, vous pouvez piocher une seule carte que vous placez dans votre main,
- Vous pouvez placer autant de cartes de votre main par tour sur le plateau, dans la limite du nombre d'emplacements de cartes disponibles sur votre côté du plateau (au maximum 4) et en respectant les sacrifices à réaliser
- A la fin de votre tour, chacune de vos cartes "animal" attaque. Si une carte de votre adversaire fait face à la carte attaquante, la carte de votre adversaire perd en nombre de points de vie le nombre de points d'attaque de votre carte. 
Si au contraire, aucune carte de votre adversaire ne se trouve face à une de vos cartes, le score est augmenté en votre faveur du nombre de points d'attaque de votre carte.
Les cartes "animal" volantes attaquent directement le score même si une carte adverse se trouve en face d'elle.

Un message devra indiquer les dégâts infligés par les attaques à la fin du tour. 

Après votre tour, votre adversaire joue de la même façon que vous (à la seule différence que vous n'avez pas à indiquer les cartes que vous jouerez au prochain tour).


### Déroulement de la partie
- Au début de la partie le joueur, prend en main les 4 premières cartes de la pioche.
- Des cartes obstacles peuvent être présentes sur le plateau au début de la partie. Elles occupent chacune un emplacement de carte, possèdent un certain nombre de points de vie et doivent être éliminées par vous ou votre adversaire avant de placer une carte à leur emplacement.
- La partie se termine lorsqu'un déséquilibre de 5 points apparaît dans le score.


### Déroulement du jeu
- Au début de la partie le joueur commence avec une pioche de 15 cartes constituée majoritairement d'écureuils.
- Le jeu est constitué de trois parties. Vous gagnez si vous remportez les trois parties.
- A la fin de la deuxième partie, vous pouvez ajouter à votre pioche une nouvelle carte parmi deux cartes proposées.

### Gestion de l'adversaire
C'est votre application qui jouera pour l'adversaire du joueur. Ses actions peuvent être déterminées entièrement à l'avance.
En revanche, évitez les stratégies aléatoires, cela risque de complexifier le debuggage et les tests de votre application.

### Liste des cartes animaux

Nom | Attaque      | Points de vie  | Gouttes de sang  | Os | Volant ? |
-------- |---------|---------|---------|----------------|-----|
Chat |0  |1  | 1  | 0         | non |    
Grizzly | 4| 6 | 3| 0 | non |
Coyote | 2 | 1 | 0 |4 | non |
Moineau | 1 | 2 | 1 | 0 | oui |
Corbeau |2 | 3| 2 | 0 | oui |
Ecureuil | 0 | 1 | 0 | 0 | non |
Hermine | 1 | 3 | 1 |0 | non |
Louveteau | 1| 1 | 1 |0  | non |
Loup |3 | 2 | 2 |0  | non |
Punaise | 1 | 2 | 0 | 2 | non |

### Liste des cartes obstacles
Nom | Points de vie      |
-------- |---------|
Rocher | 5         |     
Sapin | 3  |

## Proposition d'affichage
```
    Partie 1

    1er Tour:

         *-----------*   *************   *-----------*   *************
         | Louveteau |   *           *   | Moineau   |   *           *
         |-----------|   *           *   |-----------|   *           *
         | PV: 1     |   *           *   | PV: 1     |   *           *
         | Att: 1    |   *           *   | Att : 1   |   *           *
         |           |   *           *   | Volant    |   *           *
         *-----------*   *************   *-----------*   *************
               ||              ||              ||              ||
               \/              \/              \/              \/
         *************   *************   *************   *************     
         *           *   *           *   *           *   *           *
         *           *   *           *   *           *   *           *
         *     A1    *   *     A2    *   *     A3    *   *     A4    *
         *           *   *           *   *           *   *           *
         *           *   *           *   *           *   *           *
 Score   *************   *************   *************   *************
   0
         *************   *-----------*   *************   *************     
         *           *   | Rocher    |   *           *   *           *
         *           *   |-----------|   *           *   *           *
         *     B1    *   | PV: 5     |   *    B3     *   *     B4    *
         *           *   |           |   *           *   *           *
         *           *   |           |   *           *   *           *
         *************   *-----------*   *************   *************
                                                                              Pioche
  Votre main :                                                             *-----------* 
    1. Ecureuil   PV: 1     Att: 0    Gouttes de sang: 0  Os : 0           |           |
    2. Ecureuil   PV: 1     Att: 0    Gouttes de sang: 0  Os : 0           |           |
    3. Hermine    PV: 3     Att: 1    Gouttes de sang: 1  Os : 0           |     11    |
    4. Ecureuil   PV: 1     Att: 0    Gouttes de sang: 0  Os : 0           |   cartes  |
                                                                           |           |
                                                                           *-----------*
    
Actions possibles: 
  [fin] Terminer votre tour
  [piocher] Piocher une carte
  [placer <numero carte> <position>] Placer une carte sur le plateau

$ placer 2 B1
```



## Phase 2

### Pouvoirs 
- Nombreuses vies : reste vivant sur le plateau lorsqu'elle est sacrifiée
- Croissance : se transforme en loup au début du deuxième tour, où il est sur le plateau
- Puant : réduit de 1 l'attaque de la carte lui faisant face
- Coureur : se déplace vers d'un emplacement vers la droite après son attaque. Si l'emplacement vers la droite est bloquée, se déplace vers la gauche. Si les emplacements vers la gauche et la droite sont bloquées ne se déplace pas.
- Contact Mortel: s'il inflige des dégâts à une autre créature (donc pas à un obstacle), la créature blessée meurt 
- Piques pointues : inflige 1 point de dégât à la carte attaquante lorsqu'il est attaqué par une carte

Le nom des pouvoirs doit être affiché sur les cartes

Chacun des pouvoirs doit être testé.

### Cartes déjà présentes dans la phase 1
Nom | Attaque      | Points de vie  | Gouttes de sang  | Os | Volant ? | Pouvoir
-------- |---------|---------|---------|----------------|-----|-----------|
Chat |0  |1  | 1  | 0         | non | Nombreuses Vies
Grizzly | 4| 6 | 3| 0 | non |
Coyote | 2 | 1 | 0 |4 | non |
Moineau | 1 | 2 | 1 | 0 | oui |
Corbeau |2 | 3| 2 | 0 | oui |
Ecureuil | 0 | 1 | 0 | 0 | non |
Hermine | 1 | 3 | 1 |0 | non |
Louveteau | 1| 1 | 1 |0  | non | Croissance
Loup |3 | 2 | 2 |0  | non |
Punaise | 1 | 2 | 0 | 2 | non |Puant

### Liste des cartes obstacles
Nom | Points de vie      |
-------- |---------|
Rocher | 5         |     
Sapin | 3  |

### Nouvelles cartes 

Nom | Attaque      | Points de vie  | Gouttes de sang | Os | Volant ? | Pouvoir
-------- |---------|---------|--------|----------------|-----|-----------|
Elan |2 | 4 | 2 | 0 | Non | Coureur
Vipère | 1 |1| 2 | 0 | Non | Contact mortel
Porc-épic | 1 | 2| 1 | 0 | Non | Piques pointues


### Pierre de sacrifice
A la fin de la deuxième partie, après avoir choisi une nouvelle carte. Le joueur doit sacrifier une carte, il récupère alors son pouvoir (si la carte en possède) et peut l'ajouter à une autre carte animal.




Chaque rendu doit contenir :

- un programme qui compile dont les sources sont dans le répertoire `src/`,
- un diagramme de classes à jour placé dans le répertoire `uml/` ayant pour nom `semaine<numero>.puml`,

La structure du dépôt git doit être la suivante :
```
├── README.md
├── .gitignore
├── deps/
    ├── hamcrest-core-1.3.jar
    ├── junit-4.13.1.jar
├── out/
    ├── .gitkeep
├── src/
    ├── Main.java
    ├── ...
├── tests/
    ├── ...
├── uml/
    ├── semaine1.puml
    ├──...
```


## Contributeurs

- David
- EthanAymeric
