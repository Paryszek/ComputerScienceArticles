# Procedural Grid Generator 2D for Unity - Cellular Automata

### Introduction

Creating a procedural generated world in 2D can be a challenge, how to start? Dividing the world into grid tiles can be o good beginning, but what to do next? I asked myself the same questions and I decided to dive into Procedural Grid Generation world.

There’s a lot of algorithms that can help us generate grids, but we need to decide what we want for our specific case. I picked Cellular Automata and Running Agents algorithms.

To understand the idea better I decided to create a package for Unity Engine, this will help me in better maintenance, separation and reusability in future projects. If you wish, you can actually skip this article and checkout the code at my public Github repository, link is down below in article’s summary.

### Cellular Automata

It’s a system which consists of cells that neighbor each other in some preset pattern. Every cell can become one of the states, the number of states is finite. Current state is determined by the surrounding neighbor cell states. Rule for cell states should be constant. One synchronizing step loops through every cell and determine it’s new state. Number of synchronizing steps is finite. Every next loop iteration and different state rules can give us various outcomes. I encourage you to test different configurations and pick one that suits your case. 

As you can see idea behind Cellular Automata is quite simple, so how can we use it to generate our world? 

First we need to create 2D array grid that will consist of 0’s and 1’s. We can treat number 0 as empty square which is walk-able and number 1 as fill square which blocks movement. Simple C# enum should be enough for this task.

```csharp
public enum SquareType {
  EMPTY,
  FILL
}
```

Second we should generate noise by looping through every cell and randomly pick it’s state using constant chance value (eg. 45% chance for wall state). 

```csharp
private void GenerateNoise() {
  for (var i = 0; i < roomWidth; i++) {
    for (var j = 0; j < roomHight; j++) {
      if (Random.value > noiseDensity) {
        grid[i, j] = SquareType.FILL;
        continue;
      }

      grid[i, j] = SquareType.EMPTY;
    }
  }
}
```

*Random.value -* returns random value in range from 0 to 1, so our *noiseDensity* variable should be float and set equal to 0.45

![Noise](api/images/noise.png)

> *Generated Noise - 45% noise, 50x50 size*
> 

After we generate the noise we can proceed to first iteration loop that sets every cell state using predefined rule e.g. cell is surrounded by more than four filled neighbors, the cell state should become fill (value 1), otherwise cell should become empty (value 0).  

```csharp
private void CellularAutomata() {
  for (int iteration = 0; iteration < iterations; iteration++) {
    SquareType[,] tempGrid = (SquareType[,])grid.Clone();

    for (int i = 0; i < roomWidth; i++) {
      for (int j = 0; j < roomHight; j++) {
        var fillNumber = 0;
        var border = false;

        for (int k = i - 1; k <= i + 1; k++) {
          for (int l = j - 1; l <= j + 1; l++) {
            if (k >= 0 && l >= 0 && k < roomWidth && l < roomHight) {
              if (k != i || l != j) {
                if (tempGrid[k, l] == SquareType.FILL) {
                  fillNumber++;
                }
              }
            } else {
              border = true;
            }
          }
        }

        if (fillNumber > 4 || border) {
          grid[i, j] = SquareType.FILL;
        } else {
          grid[i, j] = SquareType.EMPTY;
        }
      }
    }
  }
}
```

*iterations -* is number of loops through every cell to determine it’s new state. You can actually pick value that suits you best, for testing reasons its set to three.

*grid.Clone(); -* return copy of the whole grid array. Its important to clone the latest grid at the beginning of each iteration to prevent overlapping with new states from previous row or column. 

*border - a*rea beyond the grid is treated as filled, so whenever cell is placed at the edge variable *border* is set to true and state of current cell is set to filled. 

For every iteration we scan through grid array cells and determine their new states by checking closest neighbors states. If there is more than four filled cells around the current cell it should become filled too, otherwise cell becomes empty. 

Now we can see the results below for each iteration.

![Iteration](api/images/iteration.png)

> *First iteration - 45% noise, 50x50 size*
> 

First iteration should give some good results of islands consists with filled cells and empty cells between. 

![Iteration1](api/images/iteration1.png)

> Second *iteration - 45% noise, 50x50 size*
> 

Second iteration removes some loose filled cells and smooth the islands edges.

![Iteration2](api/images/iteration2.png)

> *Third iteration - 45% noise, 50x50 size*
> 

Third iteration removes loose filled cells and removes smaller islands

### Summary

By changing the noise value, number of iterations and grid size, we can receive various outcomes. Once more I encourage you to work with it by yourself and see what parameters fits your case the best. Algorithm is not that complicated and can be used as foundation to produce procedurally generated game areas.

Code as unity package is available here → [https://github.com/Paryszek/ProceduralGridGenerator2D](https://github.com/Paryszek/ProceduralGridGenerator2D)