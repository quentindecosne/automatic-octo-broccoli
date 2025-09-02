# Fitness Training Programs

A structured JSON-based fitness training program system for creating and organizing workout programs across various training modalities. This repository provides examples and templates for calisthenics, strength training, mobility, and other fitness programs.

> **Note:** This repository contains JSON definitions of fitness programs intended for use with a companion fitness application. It is not a standalone workout viewer.

## 📋 Overview

This system provides:
- **Flexible program structure** for any training modality (calisthenics, strength, mobility, etc.)
- **RPE-based exercise prescriptions** for personalized intensity
- **Progressive phases** with testing and training weeks
- **Comprehensive exercise databases** with detailed descriptions
- **JSON format** for easy integration with fitness applications
- **Example programs** to demonstrate the format and structure

## 🏗️ Repository Structure

```
├── <program-name>/                # Example program directory (e.g., calisthenics-level-1, Knee Ability Zero)
│   ├── program.json               # Program structure and phases
│   ├── exercises.json             # Exercise database with descriptions
│   └── workouts/                  # Individual workout files
└── docs/                          # Documentation
    ├── PROGRAM_JSON_FORMAT.md     # Program structure specification
    ├── WORKOUT_JSON_FORMAT.md     # Workout file format
    └── EXERCISES_JSON_FORMAT.md   # Exercise database format
```

## 🚀 Getting Started

1. **Select a program** by choosing a program directory (e.g., `calisthenics-level-1`, `Knee Ability Zero`)
2. **Review the exercise database** in `<program-name>/exercises.json`
3. **Follow the program structure** defined in `<program-name>/program.json`
4. **Execute workouts** using the individual files in `<program-name>/workouts/`

### Example Workout Structure
```json
{
  "prescription": {
    "mode": "reps",
    "target": {
      "reps": {"min": 8, "max": 12}
    },
    "rpe": 7,
    "toFailure": "last",
    "tempo": {"down": 2, "pause": 1, "up": 1}
  }
}
```

## 📚 Documentation

Detailed format specifications are available in the `docs/` folder:

- **[Program Format](docs/PROGRAM_JSON_FORMAT.md)**: Complete program structure specification
- **[Workout Format](docs/WORKOUT_JSON_FORMAT.md)**: Individual workout file format
- **[Exercise Format](docs/EXERCISES_JSON_FORMAT.md)**: Exercise database schema


## 🤝 Contributing

We welcome contributions! Anyone can submit a pull request to add new programs, exercises, or enhancements.

When contributing:
1. Follow the JSON format specifications in `docs/`
2. Include comprehensive exercise descriptions
3. Validate workout file syntax and structure

## 📄 License

This training program system is designed for educational and fitness purposes. Consult with healthcare professionals before beginning any exercise program.

---