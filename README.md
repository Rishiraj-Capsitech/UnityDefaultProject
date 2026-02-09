# Unity Project Standards (Instructional Guide)
 
## Purpose
This document defines the default Unity project structure, coding rules, and UI standards to be followed by all team members. The goal is to maintain consistency, scalability, performance, and ease of maintenance across all projects.
 
---
 
## 1. Project Folder Structure (Main Branch)
This section explains how and why core folders are used.
 
## 2. Resources Folder Usage
 
### Purpose
The `Resources` folder is used for assets that must be loaded at runtime using code.
Unity allows loading assets using:
```csharp
Resources.Load<T>("Path/To/Asset");
```
 
Because of this behavior, Unity treats this folder differently than others.
 
### What SHOULD go inside Resources
- Localization files
- LevelData (ScriptableObjects)
- Small UI prefabs opened via code
- Runtime configuration data
- Required 2D / 3D assets that must be loaded dynamically
 
### Important Rules
- Use `Resources` *only* when runtime loading is required.
- Avoid placing large assets unless absolutely necessary.
- Assets placed in scenes should not be in `Resources`.
 
---
 
## 3. Scripts Folder Usage
This folder contains all custom C# code written by the team.
 
### 3.1 Managers
Used for global, persistent systems.
**Examples:**
- `GameManager`
- `FirebaseManager`
- `AdsManager`
- `AudioManager`
 
**Rules:**
- Usually marked as `DontDestroyOnLoad`.
- No UI logic inside.
- No scene-specific gameplay logic.
 
### 3.2 UI
Used for UI-only logic.
**Examples:**
- Panel controllers
- Button handlers
- Screen navigation
 
**Rules:**
- No gameplay logic.
- Communicates with Managers via events or method calls.
 
### 3.3 Level
Used for level-specific logic.
**Examples:**
- Level rules
- Spawn logic
- Level completion checks
 
### 3.4 Functional
Used for:
- Single-responsibility classes
- Helper systems
- Shared reusable logic
 
---
 
## 4. Code Rules & Naming Standards (MANDATORY)
 
| Item | Rule | Correct Example | Incorrect Example |
| :--- | :--- | :--- | :--- |
| **Script files** | PascalCase naming | `GameManager.cs` | `game_manager.cs` |
| **Class names** | PascalCase, match file name | `public class GameManager` | `class gameManager` |
| **Methods** | PascalCase | `LoadLevel()` | `load_level()` |
| **Variables** | CamelCase or underscore allowed | `playerName`, `Player_name` | `player-name` |
| **Private variables** | Prefix underscore recommended | `_currentScore` | `current-score` |
| **Constants** | ALL_CAPS_WITH_UNDERSCORE | `MAX_LEVEL` | `MaxLevel` |
| **Enums** | PascalCase | `GameState` | `game_state` |
| **Enum values** | PascalCase | `GameState.Paused` | `paused` |
| **Booleans** | Use verbs (is/has/can) | `isAlive`, `hasReward` | `aliveFlag` |
 
---
 
## 5. Scenes Folder Usage
 
### Purpose
The `Scenes` folder contains only Unity `.unity` scene files.
 
### Allowed contents
- `.unity` scene files
- `Lighting/` folder (auto-created by Unity when baking lights)
 
### Rules
- No scripts, prefabs, audio, or materials.
- `Lighting` folder exists only if baked lighting is used.
 
---
 
## 6. UI Guidelines
 
### Canvas Usage Rules (MANDATORY)
UI must use different Canvas setups depending on purpose. Do not mix render modes randomly.
 
### 6.1 Main UI / Menu / HUD Canvas (DEFAULT)
Used for:
- Menus
- Screens
- HUD (score, buttons, pause UI)
 
**Required Canvas Settings:**
- **Render Mode:** Screen Space - Camera
- **Render Camera:** Main Camera
- **Plane Distance:** 1
- **Sorting Layer:** Default
- **Order in Layer:** 0
 
**Canvas Scaler Settings:**
- **UI Scale Mode:** Scale With Screen Size
- **Reference Resolution:** 1920 x 1080
- **Screen Match Mode:** Match Width Or Height
- **Match:** 0.5
- **Reference Pixels Per Unit:** 100
 
*This setup ensures consistent UI across all screen sizes.*
 
### 6.2 Player HUD / World UI (Health Bar, Name Tag)
Used for:
- Player health bar above head
- Enemy health bars
- World-space indicators
 
**Required Canvas Settings:**
- **Render Mode:** World Space
- **Canvas attached to player or enemy**
- **Must always face the camera (Billboard logic)**
 
### 6.3 2D Game Specific Rule
For 2D games, Canvas render mode depends on UI type:
 
| UI Type | Render Mode |
| :--- | :--- |
| Main menus / overlays | Screen Space - Camera |
| Fixed HUD | Screen Space - Camera |
| Player health above head | World Space |
 
---
 
## Compliance
All new scenes, scripts, and UI must comply with this document. Any deviation requires team lead approval.
 
**Document Owner:** Tech Team
**Last Updated:** 9/02/26
