# Little Red: Sequel

**English** | [中文](README.zh-CN.md)

A story-driven RPG demo made in Unreal Engine 5, with 2D pixel characters walking through 3D scenes that use pixel-art textures. I built it on my own in about three months as my 2024 graduation project (Associate Degree in Digital Media Technology, Nanhu College, Shanghai).

![Gameplay preview](media/preview.gif)

**[Watch the full demo video](media/little-red-sequel-demo.mp4)** (6 min 35 s) · [download the MP4](https://github.com/Zeeekrom/little-red-sequel/raw/main/media/little-red-sequel-demo.mp4)

This repository holds the showcase material: the demo video, screenshots, production images and the exhibition poster. The Unreal project and the written thesis are not included.

## Contents

- [At a glance](#at-a-glance)
- [The game](#the-game)
- [Narrative design](#narrative-design)
- [Gameplay design](#gameplay-design)
- [Scenes](#scenes)
- [From concept map to finished scene](#from-concept-map-to-finished-scene)
- [Asset production](#asset-production)
- [Materials and effects](#materials-and-effects)
- [Programming](#programming)
- [Research before design](#research-before-design)
- [How the project was run](#how-the-project-was-run)
- [What is not finished](#what-is-not-finished)
- [What I took from it](#what-i-took-from-it)
- [Third-party work](#third-party-work)
- [Tools](#tools)

## At a glance

| | |
|---|---|
| Genre | Narrative RPG with exploration, quests and branching dialogue |
| Tone | A dark fairy tale that starts bleak and ends hopeful |
| Themes | Refusing a life someone else wrote, thinking for yourself, bullying, living inside a filter bubble |
| Engine | Unreal Engine 5.3 |
| Team | Solo, about three months: two of pre-production, one of assembly |
| Scale | About 199 asset sets (124 3D, 75 2D), three gameplay systems joined into one game, 20 reference games reviewed |
| Status | Playable demo. Part of the planned story is in |

## The game

Everyone in this world is born holding a fairy-tale book. For most people the pages are blank. A few are "protagonists": their book already contains their whole life, and they are expected to act it out so the story can be copied into everyone else's book as a lesson. The world itself was built by an AI, and nobody living in it knows that.

You play the newest Little Red Riding Hood. The village has rules for her: walk along the road, always wear red, and follow the prophecy in her book, which ends with her being eaten by the Big Bad Wolf. The game is about what happens when she stops following it.

| | |
|---|---|
| ![The three rules](media/gameplay/three-rules.jpg) | ![Loading screen text](media/gameplay/loading-screen-text.jpg) |
| The village's rules for Little Red, shown at the start | Loading screens carry story text |

## Narrative design

- **A familiar story with the roles questioned.** In this world the books say protagonists are always brave and good. In practice some of them are not, and some of the "villains" never chose the part. Little Red is one of the few who refuses her script.
- **Two points of view.** After Chapter 0 the player continues either as Little Red or as the Big Bad Wolf, who has started to doubt the monster his own book describes. Their storylines cross and arrive at the same goal, so the same events can be seen from both sides.
- **Branches on what the player did.** Chapters unlock on conditions. Early on, whether Little Red talked to a travelling merchant before the village chief gets to her, and whether a hidden value is above zero, decides between a branch that ends badly and a branch that leads on to the Wolf's village.
- **Chart first, text second.** I drew the whole story as a flowchart with both character lines, chapter names, unlock conditions and a summary of each chapter, and then wrote the dialogue and quests from that chart.
- **Several proposals before one story.** I wrote a set of complete story proposals (outline, main plot, theme, references) and picked this one.

A simplified view of the chart:

```mermaid
flowchart TD
    C0["Chapter 0<br/>shared opening"] --> R1["Little Red · Chapter 1<br/>The Shadow under the Red Hood"]
    C0 --> W1["The Wolf · Chapters 1-3<br/>doubts the role his book gives him"]
    R1 -- "never spoke to the travelling merchant" --> R2A["Chapter 2<br/>worn down, with nobody on her side"]
    R2A --> BE["Bad End 1"]
    R1 -- "hidden value above 0,<br/>or spoke to the merchant" --> R2B["Chapter 2<br/>disguised, she finds the Wolf's village"]
    R2B --> M["The two lines meet in the forest"]
    W1 --> M
    M --> T["They look for a way to change<br/>what the books have written"]
    T --> HE["Chapter 9 · Happy End<br/>What kind of life do you want to live?"]
```

## Gameplay design

- **Hub exploration.** The game is made of small, dense areas (the village, house interiors) where the player picks up information by walking around, examining objects and talking to villagers.
- **Hidden values.** Exploring and talking quietly raises hidden values such as courage. When one crosses a threshold, a different storyline or ending opens.
- **Indirect guidance.** The early game does not point at the truth. It lets the player notice the gap between what the villagers say and what is actually in front of them. In places the game breaks the fourth wall and speaks to the player.
- **Quests and interaction.** A quest tracker shows the current objective with a waypoint and distance. A single "walk up and press F" interaction starts dialogue, advances quests, changes scene or adjusts hidden values.

| | | |
|---|---|---|
| ![Hidden value feedback](media/gameplay/hidden-value-popup.jpg) | ![Quest tracker](media/gameplay/quest-tracker.jpg) | ![Dialogue](media/gameplay/dialogue.jpg) |
| Opening a chest raises a hidden value | Quest tracker with a waypoint and distance | Dialogue with player choices |

## Scenes

| | | |
|---|---|---|
| ![Village stage](media/gallery/01-village-stage.jpg) | ![Campfire](media/gallery/02-campfire.jpg) | ![Market stall](media/gallery/03-market-stall.jpg) |
| ![Village from above](media/gallery/04-village-from-above.jpg) | ![Island overview](media/gallery/05-island-overview.jpg) | ![Rope bridge](media/gallery/06-rope-bridge.jpg) |
| ![Cottage exterior](media/gallery/07-cottage-exterior.jpg) | ![Interior with a light shaft](media/gallery/08-interior-light-shaft.jpg) | ![Interior](media/gallery/09-interior-table.jpg) |

| | |
|---|---|
| ![Village cottage at night](media/screenshots/04-village-cottage.jpg) | ![Village stage](media/screenshots/05-village-stage.jpg) |
| Village exterior with the quest tracker and a waypoint marker | The village stage, with an interaction prompt |
| ![Home interior](media/screenshots/03-home-interior.jpg) | ![Dialogue at home](media/screenshots/07-dialogue-mother.jpg) |
| First quest completed inside the house | Dialogue with Little Red's mother |
| ![Bridge](media/screenshots/06-bridge.jpg) | ![Interior dialogue](media/screenshots/08-dialogue-interior.jpg) |
| Bridge and river on the way to the signpost | An interior scene with object dialogue |

## From concept map to finished scene

| | |
|---|---|
| ![Concept map](media/process/concept-map.jpg) | ![White-box of the island](media/process/whitebox-island.jpg) |
| 1. Top-down concept map with the positions of the main assets | 2. The same island as a white-box and as a lit scene |
| ![White-box of the village](media/process/whitebox-village.jpg) | ![Painting landscape layers](media/process/landscape-painting.jpg) |
| 3. The village: map, white-box and final layout | 4. Painting landscape layers from the player's camera angle |

1. **Concept map.** I drew a top-down map in Inkarnate and used it to decide where the main buildings and landmarks go.
2. **White-box.** In Unreal I placed the large structures (houses, the tower, bridges) and stood in boxes for everything smaller.
3. **Terrain.** A Blueprint with a camera fixed the top-down angle the player would have. Working in that view, I sculpted the terrain to match the map and painted rock, dirt, grass and gravel-path layers with a layer-blended landscape material.
4. **Materials.** Normal maps were generated from the colour textures in xNormal. In Unreal each asset got a material instance with controls for normal strength, UV, metallic, roughness and specular.
5. **Lighting.** Lights, effects, post-process volumes, exponential height fog and a sky light went in, the material instances were tuned against the lit scene, and the lighting was baked. Each interior went through the same pass.

## Asset production

| | |
|---|---|
| ![Asset list](media/process/asset-list.jpg) | ![Checking an asset in Blender](media/process/asset-check-blender.jpg) |
| Part of the asset list (in Chinese): name, scene, progress, thumbnail and white-box notes | Checking a finished bridge and its texture in Blender |
| ![Stable Diffusion settings](media/process/sd-webui-settings.jpg) | ![ComfyUI workflow](media/process/comfyui-workflow.jpg) |
| Sampler and upscale settings used for pixel textures (Chinese UI) | A ComfyUI graph tested as an alternative to the WebUI |

<img src="media/process/asset-sheet.jpg" alt="Part of the asset library" width="330">

Part of the finished asset library.

- **Look.** 2D pixel sprites in 3D environments with pixel textures, in the vein of HD-2D games. I chose it after studying indie games that mix the two, because it gave a good trade-off between production speed and quality for one person.
- **Scale.** About 199 asset sets: roughly 124 3D and 75 2D, plus visual effects, post-processing and character animation. I made more than the demo needed on purpose, so a batch that failed review would not hold up the schedule.
- **Asset list.** One sheet tracked every asset: Chinese and English name, priority, progress, the scene it belongs to, a thumbnail, the white-box design and the reference.
- **Texture pipeline.** White-box models in Maya, UVs in RizomUV, then pixel-style textures generated with Stable Diffusion (two pixel-art LoRAs merged, a pixel-style SDXL base model, img2img) and fitted to the UVs in Photoshop. This got me to about ten finished assets a day.
- **Review.** Each asset was previewed in Blender's Cycles renderer, named to a convention, and added to the sheet with a screenshot once it passed.
- **Where the pipeline stops.** Pixel art hides seams well. I did not find a reliable way to make generated textures tile cleanly, so the method is limited to this style.
- **Hand-drawn 2D.** Props, character sprites and animations were drawn in Aseprite, with the character sprites worked up from reference.
- **Audio.** The music and sound effects are not mine. Most are CC0.

## Materials and effects

| | |
|---|---|
| ![Foliage and fog materials](media/techart/foliage-and-fog-material.jpg) | ![Landscape blend material](media/techart/landscape-blend-material.jpg) |
| Material graphs for wind-driven foliage and fog | Layer-blended landscape material |

![Niagara effects](media/techart/niagara-fireflies-smoke-fire.jpg)

Niagara effects: fireflies, smoke and fire.

- **Special materials.** Foliage that moves in the wind, masking so objects between the camera and the character do not hide her, UV controls, fresnel, and fades driven by depth and camera distance.
- **Light and atmosphere.** Emissive lamps and fire, volumetric light shafts, height fog and post-process volumes, with baked lighting underneath.
- **Effects.** Fire, fireflies and smoke are Niagara systems. The startup logo and particle animations were made with After Effects and Houdini.

## Programming

Most gameplay logic is Blueprint. The quest system, the dialogue system and the main menu each started from a different Unreal Marketplace product: two C++ plugins and a menu asset. They were not made to work together, so a large part of the programming was modifying them and joining them into one game.

| | |
|---|---|
| ![Interaction Blueprint](media/blueprints/interaction.jpg) | ![Player Blueprint](media/blueprints/player.jpg) |
| Interaction: entering range shows the prompt and enables input, and pressing the key starts the dialogue | Player Blueprint: movement, and saving and loading position and quest state |
| ![Sprite animation state machine](media/blueprints/sprite-animation.jpg) | ![Main menu](media/screenshots/01-main-menu.jpg) |
| Animation Blueprint for the 2D sprite (PaperZD): stand and walk states chosen from velocity | Main menu: continue, new game, load, settings, quit |
| ![Graphics settings](media/screenshots/02-graphics-settings.jpg) | ![Save and load](media/ui/save-and-load.jpg) |
| Graphics settings: resolution, window mode, frame rate, quality presets | Save and load slots |

Menus are in Chinese and story text is in English. See [What is not finished](#what-is-not-finished).

- **Quest system.** Based on a Marketplace quest plugin: C++ classes with a node-based quest editor, several quest types, completion conditions and an on-screen tracker. I modified it for this game and wrote the quests in its editor.
- **Dialogue system.** Based on a different Marketplace plugin with a node-based editor for branching dialogue. I modified it and joined it to the quest system.
- **Main menu and saves.** Based on a Marketplace menu asset: new game, continue, load, and graphics and audio settings through Unreal's settings API, with UMG screens. I modified it and connected it to the other two systems.
- **Player.** My own Blueprint that handles movement and stores and restores position and quest state, plus an animation Blueprint for sprite movement.
- **Interaction.** One Blueprint of my own handles the "walk up and press the key" prompt for dialogue, quests, scene changes and hidden values.
- **Tested in isolation first.** Each system was built and tried in a small test project before it was moved into the game.

ChatGPT helped with parts of the C++ header changes and some Blueprint logic, and helped me iterate on story text. I corrected and integrated the results by hand. How far AI tools could help a solo developer was one of the questions the thesis set out to answer.

## Research before design

- **Game jams.** I reviewed ten entries from Ludum Dare, itch.io, Reddit game jams and Global Game Jam. For each one I wrote down how it was made, what works in it and what I could borrow. The storytelling and "meta" ideas, and the habit of keeping interaction small, came from here.
- **Commercial indie games.** I reviewed ten games from the Steam indie charts in more depth. This is where the 2D-in-3D look, the non-linear story, multiple endings and two points of view were tested against games that had already shipped them.
- **AI in games.** I kept a table of AI techniques used in game production and studied how one commercial game uses AI features.
- **Technical tests.** Before committing to a method I tested it: the texture pipeline above, and the menu, quest and dialogue systems in small demos.

## How the project was run

- **Schedule.** Two months of pre-production (research, design documents, technical tests, asset production), then one month to assemble and polish.
- **Documents.** Audience and gameplay research, story proposals, the non-linear story chart, the asset list and a survey of AI tools used in games.
- **Priorities.** When tasks competed, design documents came before code, and code before art.
- **Risk.** Assets that did not reach a usable standard in pre-production were remade in the second phase, and spare assets were produced in advance.
- **Tracking.** Each week I checked the time spent per task against the plan and adjusted.
- **Backups.** The project was versioned on GitHub every day, with two extra copies on a cloud drive and an SSD.
- **From internships.** Asset naming rules, the asset tracking sheet and the habit of testing techniques before committing to them came from my internships at game studios.

## What is not finished

- This is a demo. Only part of the planned story is playable, and some planned features were cut for time.
- Menus are in Chinese and story text is English only. Language switching was not completed.
- UI art is basic, and some screens and audio are placeholders.
- Known bug: loading a save occasionally hangs on the loading screen.

## What I took from it

- It was the first game I took from a blank page to a packaged build, and it showed me how the parts of production depend on each other.
- Studio habits scale down. Requirements, a schedule, version control and technical tests were as useful for one person as for a team.
- AI tools covered some of my gaps in design and programming and sped up texture work. They did not remove the need to check and fix what they produced.
- I deliberately spent less time on traditional art and more on technical art and programming. That shift is why I went on to study software engineering.

## Third-party work

- **Quest and dialogue systems.** Two Unreal Marketplace plugins, modified and combined.
- **Main menu, settings and save screens.** An Unreal Marketplace asset, modified.
- **Sprite animation.** The PaperZD plugin.
- **Texture generation.** Stable Diffusion with community pixel-art LoRAs and a pixel-style SDXL base model.
- **Music and sound effects.** Not mine. Most are CC0.

The story, the design documents, the environment, the asset library, the materials and effects, and the Blueprint logic that ties the systems together are my own work, with AI assistance where noted.

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
