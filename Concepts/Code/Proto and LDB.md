# Proto

Proto is an class representing most of the content the game has. All items, recipes, technologies and machines have protos. Protos are stored in a special static container called LDB (Load DataBase).

# Types of protos
### AbnormalityProto
Defines one of the checks the game uses to know if mods are installed

### AchievementProto
Defines an achievement. Uses special class called `AchievementDeterminator` to determine when achievement has been reached

### AdvisorTipProto
Defines a tip from advisor. Uses special class called `AdvisorDeterminator` to determine when advisor should give the tip

### AudioProto
Defines an audio clip that can be played. Also supports localized audio clips.

### ItemProto
Defines an item. It stores all properties that define how the item behaves and what it does. Also defines whether it can be built

### MilestoneProto
Defines a milestone the player can get. Uses special class called `MilestoneDeterminator` to determine when milestone is reached

### ModelProto
Defines all instanced models the game uses. It usually points to a prefab which contains the bulk of the data. Once the game is loaded, that data is transferred to PrefabDesc class, which can be accessed from ModelProto and ItemProto

### RecipeProto
Defines a recipe. It stores ingredients needed, time to craft and what is the result

### SignalProto
Defines an icon with a discription. Mostly used by alarm system and traffic monitor. Likely will be used for digital logic system that I think will come later.

### StringProto
Defines localization strings. Vanilla game by default supports `English`, `Chinese` and `French` languages.

### TechProto
Defines a technology. All technologies store what recipes, functions and upgrades they unlock

### ThemeProto
Defines planet theme. Stores data like what materials are used for it's terrain, what veges and ores it can contain. What are it's environment conditions.

### VegeProto
Defines a vegetation object. These are usually trees, stones, bushes, grass, etc.

### VeinProto
Defines a vein player can mine for resources.
