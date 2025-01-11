- our game state can be in variety of possible states:

  - start(idle)
  - playing
  - paused
  - won
  - lost

- for our use case we are stroing this into a type alias , but can also store into a TS enum.

- we will make a dynamic grid to insert a random unique emoji insider a Set depending on the grid size, and then duplicate them and shuffle them around.
