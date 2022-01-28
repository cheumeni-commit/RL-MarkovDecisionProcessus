# RL-MarkovDecisionProcessus

Ce projet permet de modéliser les gains pouvant être obtenu suite au lancé d'un dé à N face avec Markov Decision Processus(MDP). 
C'est une forme très simple et accessible de modélisation de l'apprentissage par renforcement (RL).

# Description du problème

1.  You start with $0$ dollars.

2.  At any time you have the option to roll the die or to quit the game.

    1.  **ROLL**:

        1.  If you roll a number not in `is_bad_side`, you receive that
            many dollars (e.g., if you roll the number $2$ and $2$ is
            not a bad side -- meaning the second element of the vector
            `is_bad_side` is $0$, then you receive $2$ dollars). Repeat
            step 2.

        2.  If you roll a number in `is_bad_side`, then you lose all the
            money obtained in previous rolls and the game ends.

    2.  **QUIT**:

        1.  You keep all the money gained from previous rolls and the
            game ends.

# Modélisation

Pour résoudre ce problème, nous avons déterminé :

- les différents états (situation) dans lesquels peut se retrouver le jouer
- les actions qui peuvent être réalisées depuis chaque états
- les gains et les pertes potentiels associés à chaque action réalisée par le jouer

Le but étant d'optimiser les gains du jeu, nous avons implémenté une variante simplifiée de l'équation de Bellman comme décrit ci-dessous.

```
     E(money, N)= max(money, (1/n)*E(money+1, N-1)+(1/n)*E(money+2, N-1 + ....+ 1/n)*E(money+k, N-1))) avec k appartient à la liste des faces gagnantes
```

avec E l'expectation attendue et money = le gain

Nous avons fait le choix, pour des raisons de rapidité d'éxécution du code, de programmer un algorithme itératif.
En effet, nous initialisation un ensemble d'états initiaux avec des grains potentiels associés. Ensuite, avec un boucle, nous parcourons l'ensembles
des états du jeu et métons à jour les gains éventuels associés aux différents transitions possible et décidons s'il est nécessaire de continuer le jeu où de le stopper et d'empaucher ses gains.


```BibTeX
@misc{jmc2022RL-MarkovDecisionProcessus,
  author =       {Jean-Michel Cheumeni},
  title =        {RL},
  howpublished = {\url{git@github.com:cheumeni-commit/RL-MarkovDecisionProcessus.git}},
  year =         {2021}
}
```