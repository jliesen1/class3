# CDS215 — Game 3: Treasure Hunt
## Independent Python Programming Challenge | Student Instructions

### Mission
Drive your blue Husky around the arena to collect **all five gold treasures** while avoiding the red guard. Each treasure is worth **10 points**, so collecting all five earns **50 points**. You must finish before the 110-second simulated-time limit. The guard patrols the arena, but may chase you when you get close.

You will complete **four programming tasks independently** inside **Part 5, `update_mission()`** of `CDS215_Treasure_Hunt_Independent_Student.py`. You may refer to your earlier Python notebooks and examples. The complicated PyBullet driving, guard navigation, collision detection, and graphics are already supplied. **Do not modify those sections.**

### Before you begin: understand the supplied variables

- `player_x` and `player_y` are your Husky's current X and Y coordinates.
- `TREASURE_SPOTS` is a list of five `(x, y)` coordinate pairs. The first number (`[0]`) is X; the second (`[1]`) is Y.
- `for index, treasure in enumerate(TREASURE_SPOTS):` is a prewritten loop that examines one treasure at a time. `index` identifies which treasure; `treasure` holds that treasure's coordinates.
- `game["collected"]` is a **set** of indexes for treasures already collected. The supplied `continue` skips those treasures.
- `game["score"]` is your running point total; `game["result"]` records whether you are playing or have won.
- `game["step"]` counts completed physics simulation steps. `PHYSICS_HZ` is the number of steps per simulated second.

### Task 1 — Calculate the distance to each uncollected treasure

The program needs to know when the Husky is close enough to collect a treasure. Inside the supplied `for` loop, replace the `float("inf")` placeholder with a calculation that uses `math.hypot()`.

Your calculation must find the horizontal difference between the player's X coordinate and this treasure's X coordinate, and the vertical difference between their Y coordinates. Store the distance in `distance`.

**Hints:** Each `treasure` is `(x, y)`. Python accesses those elements with `[0]` and `[1]`. The `math.hypot()` function takes the two coordinate differences and returns the straight-line distance. The game recalculates this as the Husky moves.

### Task 2 — Collect a treasure and award points

Write an `if` statement that decides whether a treasure may be collected. **Both** requirements must be satisfied: (a) the Husky is within `TREASURE_RADIUS`, and (b) the treasure has not already been collected.

When the condition is true, write the three indented actions: record the `index` in `game["collected"]` using `.add()`, increase `game["score"]` by `TREASURE_POINTS`, and call the already-written `celebrate_treasure(game, index)` helper. That helper removes the gold marker and announces the score; it does not award the points for you.

**Hints:** Think about `and` versus `or`, `not in`, `+=`, and indentation. A treasure must never award points a second time.

### Task 3 — Recognize when all treasures are collected

After the `for` loop, write an `if` statement that declares victory **only** when the player has earned the maximum possible score.

Use the number of treasures in `TREASURE_SPOTS` and the number of points per treasure to determine that maximum. If the player has earned it, change `game["result"]` to `"WIN"` and display the success message `MISSION COMPLETE! You collected all five treasures!`.

**Hints:** `len()` counts items. Multiplication can calculate the maximum score. Your winning condition must be **outside** the loop, so it evaluates after the available treasures have been checked.

### Task 4 — Display the completion time

Add two statements **inside Task 3's winning `if` block**. First, compute the number of **simulated seconds** from `game["step"]` and `PHYSICS_HZ`, storing the result in a new variable `completion_time`. Second, print the time using an **f-string formatted to one decimal place**.

Example output: `Completion time: 42.7 seconds`

**Hints:** How do you convert steps into seconds when you know the number of steps per second? Python's `:.1f` format displays one digit after the decimal point. The completion time should appear **only after all five treasures are collected**. You do not need to initialize `completion_time` in the game dictionary.

### Test your work

Test more than just the final victory screen. Try collecting one treasure, returning to the same spot, collecting more treasures, and finishing all five. The program should award **10 points per new treasure only**, remove a treasure when collected, show no victory before 50 points, and display the completion time only when you win.

If something does not work, check your `if` conditions, dictionary key names, indentation, and whether `distance` is correctly calculated *inside* the loop.

### Final experiment and reflection

Adjust **only** your player's speed and turning speed at first (`PLAYER_SPEED`, `PLAYER_TURN_SPEED`); keep the guard's settings unchanged. Can you collect more treasures or finish in less simulated time? Write your previously assigned **approximately 100-word reflection** explaining the settings you tested, how your collection code works, and your results. Submit your completed Python file and reflection as instructed in Canvas.

**Controls:** W/Up forward; S/Down reverse; A/Left turn left; D/Right turn right; R restart; Q quit. Click the PyBullet window first so it receives keyboard input.
