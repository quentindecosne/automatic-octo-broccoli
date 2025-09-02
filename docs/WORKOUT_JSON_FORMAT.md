# Workout JSON Format Documentation

Workout JSON files (e.g., `1A.json`, `upper-strength.json`) define individual training sessions. Each file contains exercises organized into blocks with specific prescriptions, rest periods, and execution parameters.

## File Structure

```json
{
  "id": "workout-id",
  "title": "Workout Display Name",
  "blocks": [
    {
      "type": "straight|circuit",
      "rounds": 3,
      "items": [
        {
          "id": "item-1", 
          "exerciseId": "exercise-identifier",
          "prescription": {
            "mode": "reps|time",
            "target": {
              "reps": {"min": 8, "max": 12},
              "timeSec": {"min": 30, "max": 45}
            },
            "rpe": 7,
            "tempo": {"down": 2, "pause": 1, "up": 1},
            "toFailure": "none|last|each"
          },
          "restAfterSec": 60
        }
      ],
      "restBetweenRoundsSec": 120,
      "postBlockRestSec": 180
    }
  ]
}
```

## Field Descriptions

### Workout Level

- **`id`** (required): Unique workout identifier matching filename
- **`title`** (required): Display name shown to users
- **`blocks`** (required): Array of exercise blocks

### Block Level

- **`type`** (required): `"straight"` (rest between exercises) or `"circuit"` (minimal rest between exercises)
- **`rounds`** (required): Number of times to repeat this block (1 or more)
- **`items`** (required): Array of exercises in this block
- **`restBetweenRoundsSec`** (required): Rest time between rounds in seconds
- **`postBlockRestSec`** (optional): Rest time after completing this entire block

### Item (Exercise) Level

- **`id`** (required): Unique identifier within the workout
- **`exerciseId`** (required): Reference to exercise in `exercises.json`
- **`prescription`** (required): How to perform the exercise
- **`restAfterSec`** (optional): Rest after this exercise (mainly used in circuits)

### Prescription Object

- **`mode`** (required): `"reps"` or `"time"`
- **`target`** (required): Target ranges for reps or time
- **`rpe`** (optional): Rate of Perceived Exertion (1-10 scale)
- **`tempo`** (optional): Movement timing
- **`toFailure`** (optional): Failure protocol

## Target Specifications

### Reps Mode
```json
{
  "mode": "reps",
  "target": {
    "reps": {"min": 8, "max": 12}
  }
}
```

### Max Reps (No Upper Limit)
```json
{
  "mode": "reps", 
  "target": {
    "reps": null
  }
}
```

### Time Mode
```json
{
  "mode": "time",
  "target": {
    "timeSec": {"min": 30, "max": 45}
  }
}
```

## RPE (Rate of Perceived Exertion)

Scale from 1-10:
- **1-3**: Very easy, could do many more reps
- **4-5**: Easy to moderate effort
- **6-7**: Moderate to hard effort
- **8-9**: Hard, only 1-2 reps left in tank
- **10**: Maximum effort, complete failure

```json
"rpe": 8
```

## Tempo Specification

Controls movement speed:
- **`down`**: Lowering/eccentric phase (seconds or "X" for explosive)
- **`pause`**: Pause at bottom (seconds)
- **`up`**: Lifting/concentric phase (seconds or "X" for explosive)

```json
"tempo": {"down": 3, "pause": 1, "up": 1}
"tempo": {"down": 2, "pause": 0, "up": "X"}
```

## To Failure Options

- **`"none"`**: Stop at target reps/time
- **`"last"`**: Go to failure only on the last round
- **`"each"`**: Go to failure on every round

## Block Types

### Straight Sets
Exercises performed one at a time with full rest between each:

```json
{
  "type": "straight",
  "rounds": 3,
  "items": [
    {
      "id": "1",
      "exerciseId": "pull-up", 
      "prescription": {
        "mode": "reps",
        "target": {"reps": {"min": 5, "max": 8}},
        "rpe": 8
      }
    }
  ],
  "restBetweenRoundsSec": 180
}
```

### Circuit Training
Exercises performed back-to-back with minimal rest:

```json
{
  "type": "circuit",
  "rounds": 3,
  "items": [
    {
      "id": "1",
      "exerciseId": "push-up",
      "prescription": {
        "mode": "reps", 
        "target": {"reps": {"min": 10, "max": 15}}
      },
      "restAfterSec": 15
    },
    {
      "id": "2", 
      "exerciseId": "bodyweight-squat",
      "prescription": {
        "mode": "reps",
        "target": {"reps": {"min": 15, "max": 20}} 
      },
      "restAfterSec": 15
    }
  ],
  "restBetweenRoundsSec": 120
}
```

## Complete Workout Examples

### Strength Training Session

```json
{
  "id": "upper-strength-1",
  "title": "Upper Body Strength A",
  "blocks": [
    {
      "type": "straight",
      "rounds": 4,
      "items": [
        {
          "id": "main-1",
          "exerciseId": "pull-up",
          "prescription": {
            "mode": "reps",
            "target": {"reps": {"min": 3, "max": 6}},
            "rpe": 8,
            "tempo": {"down": 2, "pause": 1, "up": 1},
            "toFailure": "last"
          }
        }
      ],
      "restBetweenRoundsSec": 180,
      "postBlockRestSec": 120
    },
    {
      "type": "straight", 
      "rounds": 3,
      "items": [
        {
          "id": "accessory-1",
          "exerciseId": "push-up",
          "prescription": {
            "mode": "reps",
            "target": {"reps": {"min": 8, "max": 12}},
            "rpe": 7
          }
        }
      ],
      "restBetweenRoundsSec": 120
    }
  ]
}
```

### Circuit Conditioning

```json
{
  "id": "conditioning-circuit",
  "title": "Full Body Circuit",
  "blocks": [
    {
      "type": "circuit",
      "rounds": 4,
      "items": [
        {
          "id": "c1",
          "exerciseId": "burpee", 
          "prescription": {
            "mode": "reps",
            "target": {"reps": {"min": 5, "max": 8}}
          },
          "restAfterSec": 10
        },
        {
          "id": "c2",
          "exerciseId": "mountain-climber",
          "prescription": {
            "mode": "time", 
            "target": {"timeSec": {"min": 20, "max": 30}}
          },
          "restAfterSec": 10
        },
        {
          "id": "c3",
          "exerciseId": "jump-squat",
          "prescription": {
            "mode": "reps",
            "target": {"reps": {"min": 10, "max": 15}}
          },
          "restAfterSec": 10
        }
      ],
      "restBetweenRoundsSec": 90
    }
  ]
}
```

### Skill/Test Session

```json
{
  "id": "handstand-test",
  "title": "Handstand Assessment", 
  "blocks": [
    {
      "type": "straight",
      "rounds": 3,
      "items": [
        {
          "id": "test-1",
          "exerciseId": "wall-handstand-hold",
          "prescription": {
            "mode": "time",
            "target": {"timeSec": null},
            "toFailure": "each"
          }
        }
      ],
      "restBetweenRoundsSec": 180
    },
    {
      "type": "straight",
      "rounds": 1,
      "items": [
        {
          "id": "test-2", 
          "exerciseId": "freestanding-handstand",
          "prescription": {
            "mode": "reps",
            "target": {"reps": null},
            "toFailure": "each"
          }
        }
      ],
      "restBetweenRoundsSec": 0
    }
  ]
}
```

## Validation Rules

The app validates:
- All required fields are present
- Block types are valid ("straight" or "circuit") 
- Rounds are positive integers
- Rest periods are non-negative integers
- Prescription mode matches target specification
- RPE is between 1-10 if specified
- Exercise IDs exist in exercises.json
- Item IDs are unique within workout

## Best Practices

### Exercise Ordering
1. **Skill work first**: Handstands, levers when fresh
2. **Main strength**: Hardest exercises early in session  
3. **Accessory work**: Supporting exercises
4. **Conditioning**: Metabolic work at the end

### Block Organization
- **Group similar exercises**: Push/pull, upper/lower
- **Manage fatigue**: Don't exhaust muscles needed for later exercises
- **Progress logically**: Warm-up → main work → cool down

### Rest Periods
- **Strength work**: 2-5 minutes between sets
- **Hypertrophy**: 1-3 minutes between sets  
- **Circuits**: 15-60 seconds between exercises
- **Between rounds**: 1-3 minutes depending on intensity

## File Naming

Workout files should be named to match their IDs:
- `1A.json` for workout with `"id": "1A"`
- `upper-strength.json` for workout with `"id": "upper-strength"`
- Place all workout files in the `workouts/` directory