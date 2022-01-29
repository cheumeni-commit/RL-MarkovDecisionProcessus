# RL-MarkovDecisionProcessus

Ce projet permet de modéliser les gains obtenus suite à différents lancés d'un dé à N face. Nous appuyons sur le Markov Decision Processus(MDP). Cette méthode utilisée pour modéliser ce jeu, est une forme très simple et accessible de modélisation que nous pouvons ranger dans la famille du Rienforcement Learning(RL).

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

- les différents états (situation) dans lesquels peut se retrouver le jouer {1, 2,....., N}
- les actions qui peuvent être réalisées depuis chaque états {"go", "stop"}
- les gains et les pertes potentiels associés à chaque action réalisée par le jouer 0 <= X < N

Le but étant d'optimiser les gains du jeu, nous avons implémenté une variante simplifiée de l'équation de Bellman comme décrit ci-dessous.

```BibTeX
     E(money, N)= max(money, (1/n)*E(money+1, N-1)+(1/n)*E(money+2, N-1 + ....+ 1/n)*E(money+k, N-1))) avec k appartient à la liste des faces gagnantes
```
Cette formule est illustrée ci-dessous avec ce bout de code :

```BibTeX
for gos_left in range(1, self.max +1):
    next=[0]*len(expected)
    for money in range(LENGTH-gos_left*self.lenght):
        next[money]= max(expected[money], \
            (1./self.lenght)*sum([expected[money+k] for k in gain])) # decision stop or go

    if sum(next) != 0:
        expected=next
    else:
        break;
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