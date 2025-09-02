# exercises.json Format Documentation

The `exercises.json` file contains information about exercises used in workouts. This data is used to display detailed exercise information when users tap the info button during workouts.

## File Structure

```json
{
  "exerciseId1": {
    "name": "Exercise Display Name",
    "description": "Detailed description of the exercise",
    "instructions": [
      "Step 1: Setup instructions",
      "Step 2: Movement instructions",
      "Step 3: Additional cues"
    ],
    "tips": [
      "Performance tip 1",
      "Common mistake to avoid"
    ],
    "muscles": ["primary", "secondary", "stabilizer"],
    "equipment": ["bodyweight", "pull-up-bar"],
    "difficulty": "beginner|intermediate|advanced",
    "video": "optional-video-filename.mp4",
    "images": ["optional-image1.jpg", "optional-image2.jpg"]
  }
}
```

## Field Descriptions

### Required Fields

- **`exerciseId`** (object key): Unique identifier matching workout exercise references
- **`name`**: Human-readable exercise name displayed in the app
- **`description`**: Detailed explanation of the exercise and its benefits

### Optional Fields

- **`instructions`** (array): Step-by-step instructions for performing the exercise
- **`tips`** (array): Additional coaching cues, form tips, or common mistakes to avoid
- **`muscles`** (array): Muscle groups targeted (primary, secondary, stabilizers)
- **`equipment`** (array): Required equipment (use "bodyweight" for no equipment)
- **`difficulty`**: Skill level required (`"beginner"`, `"intermediate"`, `"advanced"`)
- **`video`**: Video filename (if included in program folder)
- **`images`**: Array of image filenames (if included in program folder)

## Complete Example

```json
{
  "push-up": {
    "name": "Push-Up",
    "description": "A fundamental upper body pushing exercise that targets the chest, shoulders, and triceps while engaging the core for stability.",
    "instructions": [
      "Start in a plank position with hands slightly wider than shoulder-width",
      "Lower your body until your chest nearly touches the floor",
      "Keep your body in a straight line from head to heels",
      "Push back up to the starting position"
    ],
    "tips": [
      "Keep your core tight throughout the movement",
      "Don't let your hips sag or pike up",
      "Full range of motion is key - go all the way down and up"
    ],
    "muscles": ["chest", "shoulders", "triceps", "core"],
    "equipment": ["bodyweight"],
    "difficulty": "beginner"
  },
  
  "pull-up": {
    "name": "Pull-Up", 
    "description": "A compound pulling exercise that primarily targets the latissimus dorsi and biceps, while also engaging the rhomboids and middle trapezius.",
    "instructions": [
      "Hang from a pull-up bar with hands slightly wider than shoulder-width",
      "Use an overhand grip with palms facing away",
      "Pull your body up until your chin clears the bar",
      "Lower back down with control to full arm extension"
    ],
    "tips": [
      "Engage your lats by pulling your shoulders down and back",
      "Avoid swinging or using momentum", 
      "Focus on controlled movement both up and down"
    ],
    "muscles": ["lats", "biceps", "rhomboids", "middle-traps"],
    "equipment": ["pull-up-bar"],
    "difficulty": "intermediate"
  },
  
  "archer-push-up": {
    "name": "Archer Push-Up",
    "description": "An advanced unilateral pushing exercise that shifts weight to one arm while the other provides minimal assistance, building single-arm strength.",
    "instructions": [
      "Start in a wide push-up position with hands wider than shoulders",
      "Lower down while shifting weight to one arm",
      "Keep the supporting arm straight and extended to the side",
      "Push back up and repeat, or alternate sides"
    ],
    "tips": [
      "Keep the non-working arm straight throughout",
      "Maintain body alignment - don't rotate the torso",
      "Start with small shifts in weight before going full range"
    ],
    "muscles": ["chest", "shoulders", "triceps", "core"],
    "equipment": ["bodyweight"],
    "difficulty": "advanced"
  }
}
```

## Exercise ID Naming Conventions

- Use lowercase with hyphens: `"push-up"`, `"pull-up"`, `"archer-push-up"`
- Be descriptive but concise: `"diamond-push-up"` not `"close-grip-push-up"`
- Use consistent terminology across your program

## Equipment Values

Common equipment values to maintain consistency:

- `"bodyweight"` - No equipment needed
- `"pull-up-bar"` - Standard pull-up bar
- `"rings"` - Gymnastics rings  
- `"parallettes"` - Low parallel bars
- `"resistance-band"` - Resistance bands
- `"wall"` - Wall for wall-assisted exercises

## Muscle Group Values

Common muscle group names:

- `"chest"`, `"shoulders"`, `"triceps"`, `"biceps"`
- `"lats"`, `"rhomboids"`, `"traps"`, `"middle-traps"`
- `"core"`, `"abs"`, `"obliques"`
- `"glutes"`, `"quads"`, `"hamstrings"`, `"calves"`

## Notes

- The `exercises.json` file is optional - exercises without entries will simply not show the info button
- All fields except the exercise ID key, name, and description are optional
- File should be placed in the root of your program directory alongside `program.json`