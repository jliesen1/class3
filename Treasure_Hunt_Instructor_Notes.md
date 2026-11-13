# CDS215 — Treasure Hunt | Instructor Answer Key and Teaching Notes

Use the student file and independent instructions for learners. Keep this document and the Instructor.py version private until students have completed their work.

## Task 1 — Distance

```python
distance = math.hypot(player_x - treasure[0],
                      player_y - treasure[1])
```

## Task 2 — Pickup, set membership, points, visual removal

```python
if distance < TREASURE_RADIUS and index not in game["collected"]:
    game["collected"].add(index)
    game["score"] += TREASURE_POINTS
    celebrate_treasure(game, index)
```

## Tasks 3 and 4 — Victory and completion time

These statements go **after the `for` loop**. Task 4 is indented **inside** the Task 3 win condition.

```python
if game["score"] == len(TREASURE_SPOTS) * TREASURE_POINTS:
    game["result"] = "WIN"
    print("MISSION COMPLETE! You collected all five treasures!")

    completion_time = game["step"] / PHYSICS_HZ
    print(f"Completion time: {completion_time:.1f} seconds")
```

## Teaching points

- `math.hypot()` calculates distance using X and Y differences; it does not magically know the treasure positions.
- `enumerate()` returns both index and coordinate pair so the pickup can be tracked.
- `game["collected"]` is a set; `continue` skips previously collected treasure indexes. The second membership check inside the `if` is an extra safeguard/illustration.
- `game["step"] / PHYSICS_HZ` returns *simulated* seconds, not clock/wall time.
- The main loop calls `update_mission()` once each simulation step **only while the game is still playing**. A prewritten guard at the start of that function also skips updates after a win, so the completion-time message prints once.
- The instructor version has the actual gameplay mechanics and answers. Student version is syntactically valid but won't collect treasure until Tasks 1–3 are completed.

## Suggested independent 35–45-minute format

Give learners the student script and instructions without showing the solution. Spend a few minutes explaining the game dictionary and `enumerate()`, then let them implement Tasks 1–4. Circulate with hints rather than giving exact statements. Reserve time for testing the scoring behavior, experimenting with player speeds, and writing the existing approximately 100-word reflection. Grade the coding logic, tests, and analysis rather than requiring every student to beat the guard.

## Verification

The scripts pass Python syntax checks. The rules are checked with mocked PyBullet methods; actual GUI/gameplay must be tested on a machine with PyBullet installed.
