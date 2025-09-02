# program.json Format Documentation

The `program.json` file defines the overall structure of a training program, including phases, weeks, and the workout schedule. This is the main configuration file that organizes how workouts are presented to users over time.

## File Structure

```json
{
  "programId": "unique-program-identifier",
  "programTitle": "Human Readable Program Name",
  "contentVersion": "1.0",
  "phases": [
    {
      "id": "P1",
      "title": "Phase Name",
      "weeks": [
        {
          "weekNumber": 1,
          "pattern": ["workout-id-1", "REST", "workout-id-2"]
        }
      ]
    }
  ]
}
```

## Field Descriptions

### Program Level

- **`programId`** (required): Unique identifier for the program (kebab-case recommended)
- **`programTitle`** (required): Display name shown to users
- **`contentVersion`** (required): Version string for program format compatibility
- **`phases`** (required): Array of training phases

### Phase Level

- **`id`** (required): Short phase identifier (e.g., "P1", "P2", "Foundation")
- **`title`** (required): Human-readable phase name
- **`weeks`** (required): Array of individual weeks in this phase

### Week Level

- **`weekNumber`** (required): Week number within the phase (1, 2, 3, etc.)
- **`pattern`** (required): Array of workout IDs and rest days for that week

## Pattern Array

The `pattern` array defines what happens each day of the week:

- **Workout IDs**: Reference to workout files (e.g., `"1A"` → `workouts/1A.json`)
- **`"REST"`**: Rest day (case-insensitive)
- **Order matters**: First item = Day 1, second item = Day 2, etc.

## Complete Example

```json
{
  "programId": "progressive-calisthenics",
  "programTitle": "Progressive Calisthenics Program",
  "contentVersion": "1.0",
  "phases": [
    {
      "id": "P1",
      "title": "Foundation Phase",
      "weeks": [
        {
          "weekNumber": 1,
          "pattern": ["assessment-upper", "assessment-lower"]
        },
        {
          "weekNumber": 2,
          "pattern": ["1A", "REST", "1B", "REST"]
        },
        {
          "weekNumber": 3,
          "pattern": ["1A", "REST", "1B", "REST", "1C"]
        },
        {
          "weekNumber": 4,
          "pattern": ["1A", "1B", "REST", "1A"]
        }
      ]
    },
    {
      "id": "P2", 
      "title": "Strength Development Phase",
      "weeks": [
        {
          "weekNumber": 1,
          "pattern": ["2A", "REST", "2B", "REST", "2C"]
        },
        {
          "weekNumber": 2,
          "pattern": ["2A", "2B", "REST", "2C", "2A"]
        },
        {
          "weekNumber": 3,
          "pattern": ["2A", "2B", "2C", "REST", "2A", "2B"]
        }
      ]
    },
    {
      "id": "P3",
      "title": "Peak Phase", 
      "weeks": [
        {
          "weekNumber": 1,
          "pattern": ["3A", "REST", "3B", "REST", "test-upper"]
        },
        {
          "weekNumber": 2,
          "pattern": ["3A", "3B", "REST", "test-lower", "REST"]
        }
      ]
    }
  ]
}
```

## Program Structure Patterns

### Assessment/Test Weeks
```json
{
  "weekNumber": 1,
  "pattern": ["test-upper", "test-lower", "test-conditioning"]
}
```

### Regular Training
```json
{
  "weekNumber": 2,
  "pattern": ["upper-strength", "REST", "lower-strength", "REST", "conditioning"]
}
```

### Intensification
```json
{
  "weekNumber": 4,
  "pattern": ["upper-strength", "lower-strength", "upper-strength", "REST"]
}
```

### Deload/Recovery
```json
{
  "weekNumber": 5,
  "pattern": ["light-movement", "REST", "mobility", "REST", "REST"]
}
```

## Naming Conventions

### Program IDs
- Use kebab-case: `"beginner-strength"`, `"advanced-handstand"`
- Be descriptive: `"push-pull-legs"` not `"ppl"`

### Phase IDs
- Short and clear: `"P1"`, `"P2"` or `"Foundation"`, `"Strength"`
- Consistent within program

### Workout IDs
- Match exactly with workout JSON filenames (without .json extension)
- Common patterns:
  - `"1A"`, `"1B"`, `"1C"` (phase + session)
  - `"upper-1"`, `"lower-1"` (descriptive)
  - `"test-push"`, `"test-pull"` (assessment workouts)

## Workout File Requirements

Each workout ID in patterns must have a corresponding JSON file:

- `"1A"` → `workouts/1A.json`
- `"upper-strength"` → `workouts/upper-strength.json` 
- `"test-push"` → `workouts/test-push.json`

## Phase Progression

Phases are presented to users sequentially:
1. User completes all weeks in Phase 1
2. Automatically progresses to Phase 2
3. Continues through all phases
4. Program completion

## Validation Rules

The app validates:
- All required fields are present
- Phase IDs are unique within program
- Week numbers are positive integers
- Patterns are not empty
- Referenced workout files exist

## Notes

- Weeks don't have to be exactly 7 days - patterns can be any length
- Users can repeat weeks or phases if desired
- Programs can have unlimited phases and weeks
- Rest days are automatically handled by the app