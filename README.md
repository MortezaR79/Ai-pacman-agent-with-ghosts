# AI-Packman-Agent-with-ghosts

In this project, you will design an agent for the classic Pacman game, which this time also includes ghosts. In this way, we used minimax search and possible minimax and designed an evaluation function.
Similar to the previous project, you can run the following command to debug and test the correctness of the algorithms:

```
python autograder.py
```

## project structure

- Pacman Agent Algorithms: Navigating and Optimizing Food Collection
  - multiAgents.py : It includes all multi-factor search factors.
- Gameboard Dynamics: Visualization, Movement, and Logic of the Pacman World
  - pacman.py : The main file that runs Pacman games. This file describes the GameState class for the Pacman game that you use in this project.
  - The implemented logic for the Pacman world is in this file. It includes various classes like AgentState, Agent, Grid, and Direction.
  - util.py : Useful data structures for implementing search algorithms are located in this file.
  - graphicsDisplay.py : Graphics for the Pacman game are implemented in this file.
  - graphicsUtils.py : Provides assistance for the graphical aspects of the game.
  - textDispaly.py : Offers ASCII-based graphics for the Pacman game.
  - ghostAgent.py : Manages the behavior of the ghost characters.
  - layout.py : Program to read map files and save their information.

The project has more files in it, but the main focus is on multiAgents.py.

## ReflexAgent

We modified the evaluationFunction so it considers both the action's result and the secondary state, not just the final state. It starts by getting key info like Pacman's new position (newPos) or the food state after the action (newFood) from GameState. The ReflexAgent should use this info to decide the best move, aiming to win on the testClassic map. To verify this, you can run the command provided below.

```
python pacman.py -p ReflexAgent -l testClassic
```

To test the agent on the mediumClassic map with one or two ghosts and run the game at high speed, use the following commands:

```
python pacman.py --frameTime 0 -p ReflexAgent -k 1
```

```
python pacman.py --frameTime 0 -p ReflexAgent -k 2
```

## Minimax

The agent needs to work well no matter how many ghosts there are. To do this, you need to have one minimum layer for each ghost and just one maximum layer for Pacman. The minimax tree should be expanded to the depth you want, and its ends should be checked with the right function. For this, the MinimaxAgent class inherits from MultiAgentSearchAgent, which includes self.evaluationFunction and self.depth. You should use these for the depth and leaf evaluation in MinimaxAgent. The default evaluation function is scoreEvaluationFunction, which you can find in the same multiAgents.py file. You can test the agent using the command provided below.

```
python pacman.py -p MinimaxAgent -l minimaxClassic -a depth=4
```

## Alpha-beta pruning

We have enhanced minimax tree traversal by adding alpha-beta pruning.
This is done through the AlphaBetaAgent class. Keep in mind, we'll still have multiple min layers (for each ghost) and one max layer (for Pacman). This improvement leads to a significant speed boost. You can verify this by running the command below for depth 3 and comparing it with the MinimaxAgent agent at depth 2. Both should finish around the same time.

```
python pacman.py -p AlphaBetaAgent -a depth=3 -l smallClassic
```

## Expectiminimax

In minimax and alpha-beta pruning, it's assumed the opponent always makes the best moves, which isn't always true. Modeling the agent's behavior to account for non-optimal choices can lead to better outcomes. Random ghosts don't always make optimal choices, so using minimax search to model them might not yield the best results. The expectiminimax method, instead of focusing on the opponent's smallest moves, considers a model of the probability of moves. To simplify your probabilistic model, imagine the ghosts choose their movements from their 4 allowed options uniformly and randomly. You can use the following command to see the agent's performance.

```
python pacman.py -p ExpectimaxAgent -l minimaxClassic -a depth=3
```

We've developed a more effective evaluation function for Pacman in betterEvaluationFunction. This function should assess the states rather than the actions. It's designed to complete the smallClassic scenario with a random ghost in half the time and win at a search depth of 2.

```
python autograder.py -q q5
```
