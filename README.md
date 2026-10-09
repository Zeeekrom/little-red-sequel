# Little Red: Sequel

**English** | [中文](README.zh-CN.md)

A story-driven RPG demo made in Unreal Engine 5, with 2D pixel characters walking through 3D scenes that use pixel-art textures. I built it on my own in about three months as my 2024 graduation project (Associate Degree in Digital Media Technology, Nanhu College, Shanghai).

![Gameplay preview](media/preview.gif)

**[Watch the full demo video](media/little-red-sequel-demo.mp4)** (6 min 35 s) · [download the MP4](https://github.com/Zeeekrom/little-red-sequel/raw/main/media/little-red-sequel-demo.mp4)

This repository holds the showcase material: the demo video, screenshots and the exhibition poster. The Unreal project and the written thesis are not included.

## The game

Everyone in this world is born holding a fairy-tale book. For most people the pages are blank. A few are "protagonists": their book already contains their whole life, and they are expected to act it out so the story can be copied into everyone else's book as a lesson. The world itself was built by an AI, and nobody living in it knows that.

You play the newest Little Red Riding Hood. The village has rules for her: walk along the road, always wear red, and follow the prophecy in her book, which ends with her being eaten by the Big Bad Wolf. The game is about what happens when she stops following it.

| | |
|---|---|
| Genre | Narrative RPG with exploration, quests and branching dialogue |
| Tone | A dark fairy tale that starts bleak and ends hopeful |
| Themes | Refusing a life someone else wrote, thinking for yourself, bullying, living inside a filter bubble |
| Engine | Unreal Engine 5.3 |
| Team | Solo, about three months |

## Screenshots

| | |
|---|---|
| ![Village cottage at night](media/screenshots/04-village-cottage.jpg) | ![Village stage](media/screenshots/05-village-stage.jpg) |
| Village exterior with the quest tracker and a waypoint marker | The village stage, with an interaction prompt |
| ![Home interior](media/screenshots/03-home-interior.jpg) | ![Dialogue at home](media/screenshots/07-dialogue-mother.jpg) |
| First quest completed inside the house | Dialogue with Little Red's mother |
| ![Bridge](media/screenshots/06-bridge.jpg) | ![Interior dialogue](media/screenshots/08-dialogue-interior.jpg) |
| Bridge and river on the way to the signpost | An interior scene with object dialogue |
| ![Main menu](media/screenshots/01-main-menu.jpg) | ![Graphics settings](media/screenshots/02-graphics-settings.jpg) |
| Main menu: continue, new game, load, settings, quit | Graphics settings panel |

Menus are in Chinese and story text is in English. See [What is not finished](#what-is-not-finished).

## Narrative design

- **A familiar story with the roles questioned.** In this world the books say protagonists are always brave and good. In practice some of them are not, and some of the "villains" never chose the part. Little Red is one of the few who refuses her script.
- **Non-linear structure.** Chapters unlock on conditions and the story has several endings. I drew the whole thing as a flowchart first, with both character lines, chapter names, unlock conditions and a summary of each chapter, and then wrote the dialogue and quests from that chart.
- **Two points of view.** After Chapter 0 the player continues either as Little Red or as a second character with the opposite outlook. Their storylines cross and arrive at the same goal, so the same events can be seen from both sides.
- **Process.** I wrote several complete story proposals (outline, main plot, theme, references) before choosing this one.

## Gameplay design

- **Hub exploration.** The game is made of small, dense areas (the village, house interiors) where the player picks up information by walking around, examining objects and talking to villagers.
- **Hidden values.** Exploring and talking quietly raises hidden values. When one crosses a threshold, a different storyline or ending opens. The player never sees the numbers.
- **Indirect guidance.** The early game does not point at the truth. It lets the player notice the gap between what the villagers say and what is actually in front of them. In places the game breaks the fourth wall and speaks to the player, and loading screens carry story text.
- **Quests and interaction.** A quest tracker shows the current objective with a waypoint and distance. A single "walk up and press F" interaction starts dialogue, advances quests, changes scene or adjusts hidden values.

## Art and technical art

- **Look.** 2D pixel sprites in 3D environments with pixel textures, in the vein of HD-2D games. I chose it after studying indie games that mix the two, because it gave a good trade-off between production speed and quality for one person.
- **Scale.** About 199 asset sets: roughly 124 3D and 75 2D, plus visual effects, post-processing and character animation.
- **Texture pipeline.** White-box models in Maya, UVs in RizomUV, then pixel-style textures generated with Stable Diffusion (two pixel-art LoRAs merged, a pixel-style SDXL base model, img2img) and fitted to the UVs in Photoshop. Normal maps were generated in xNormal and materials set up as instances in Unreal. This got me to about ten finished assets a day.
- **Hand-drawn 2D.** Props, character sprites and animations were drawn in Aseprite, with the character sprites worked up from reference.
- **Materials and effects.** Foliage that moves in the wind, masking so objects between the camera and the character do not hide her, fresnel and depth fades, emissive lights and fire. Fire, fireflies and smoke are Niagara effects.
- **Environment.** A top-down concept map drawn in Inkarnate, a white-box pass in Unreal, then a layer-blended landscape material, baked lighting, height fog and post-process volumes.
- **Audio.** The music and sound effects are not mine. Most are CC0.

## Programming

Most gameplay logic is Blueprint. The quest and dialogue systems are C++ classes exposed to Blueprint.

- **Quest system.** C++ classes with a node-based quest editor: several quest types, completion conditions and an on-screen tracker.
- **Dialogue system.** C++ classes with a node-based editor for branching dialogue, linked to the quest system.
- **Main menu and saves.** New game, continue and load. Saving and loading use Blueprint classes, interfaces, structs and data tables. Graphics and audio settings go through Unreal's settings API. The UI is built in UMG.
- **Player.** A controller that stores and restores position and quest state, plus an animation Blueprint for sprite movement.
- **Reuse.** The menu and save systems are self-contained and can be moved into another project.

ChatGPT helped draft parts of the C++ headers and some Blueprint logic, and helped me iterate on story text. I corrected and integrated the results by hand. How far AI tools could help a solo developer was one of the questions the thesis set out to answer.

## How the project was run

- **Schedule.** Two months of pre-production (research, design documents, technical tests, asset production), then one month to assemble and polish.
- **Research first.** Before designing anything I reviewed ten game-jam entries (Ludum Dare, itch.io, Global Game Jam) and ten commercial indie games from the Steam charts, and wrote down what was worth borrowing from each.
- **Documents.** Audience and gameplay research, story proposals, the non-linear story chart, an art asset list (name, priority, scene, white-box, reference) and a survey of AI tools used in games.
- **Priorities.** When tasks competed, design documents came before code, and code before art.
- **Tracking.** Each week I checked the time spent per task against the plan and adjusted. The project was versioned on GitHub with two extra backups.
- **From internships.** Asset naming rules, the asset tracking sheet and the habit of testing techniques before committing to them came from my internships at game studios.

## What is not finished

- This is a demo. Only part of the planned story is playable, and some planned features were cut for time.
- Menus are in Chinese and story text is English only. Language switching was not completed.
- UI art is basic, and some screens and audio are placeholders.
- Known bug: loading a save occasionally hangs on the loading screen.

## Tools

Unreal Engine 5.3, Visual Studio 2022, Maya 2024, Blender 4.1, RizomUV, Houdini 20, Substance 3D Painter and Designer, xNormal, Aseprite, Stable Diffusion WebUI, ComfyUI, Photoshop, After Effects, Inkarnate.

## Poster

<img src="media/poster.jpg" alt="Graduation exhibition poster" width="520">

This is the English version of the poster made for the 2024 graduation exhibition. Contact details on the original have been removed.

## Thesis

The project was submitted with a thesis written in Chinese: *Innovative Applications of Digital Media Technology in the Game Industry: The Case of Indie Games* (May 2024). It is not published here.

## Rights and contact

© 2024 Yuxiang (Evan) Huang. The video, screenshots and poster are shared for portfolio viewing. Please ask before reusing them.

Contact: [LinkedIn](https://www.linkedin.com/in/evan-h-165976301/)
