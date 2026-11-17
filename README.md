# Little Red: Sequel

**English** · [简体中文](README.zh-CN.md)

![Unreal Engine 5.3](https://img.shields.io/badge/Unreal%20Engine-5.3-313131)
![Solo graduation project, 2024](https://img.shields.io/badge/solo%20graduation%20project-2024-A4271C)

Little Red: Sequel is a story-driven RPG demo made in Unreal Engine 5. 2D pixel characters walk through hand-built 3D scenes that use pixel-art textures. You play the newest Little Red Riding Hood. The village has rules for her: walk along the road, always wear red, and follow the prophecy in her book, which ends with her being eaten by the Big Bad Wolf. The game is about what happens when she stops following it. This page shows how it was made: the story and its branches, the scenes, the asset pipeline and the systems behind them.

AI tools helped, and this page says where. Stable Diffusion generated the pixel textures, which I then fitted to each model's UVs in Photoshop. ChatGPT helped with parts of the C++ header changes, some Blueprint logic and the story text, and I corrected and integrated the results by hand. How far AI tools could help a solo developer was one of the questions the thesis set out to answer.

This is a solo graduation project from 2024, made in about three months for an Associate Degree in Digital Media Technology (Nanhu College, Shanghai). It is a playable demo with part of the planned story in. It is not a finished game.

This repository holds showcase material only: the project film, the gameplay demo video, screenshots, production images and the exhibition poster. The Unreal project is not included. The project was submitted with a thesis written in Chinese, *Innovative Applications of Digital Media Technology in the Game Industry: The Case of Indie Games* (May 2024), which is not published here.

<table>
<tr>
<td><a href="https://zeeekrom.github.io/little-red-sequel/film/"><img src="film/preview.jpg" alt="Play the 3-minute project film of Little Red: Sequel" width="520"></a></td>
<td><a href="media/poster.jpg"><img src="media/poster.jpg" alt="Little Red: Sequel graduation exhibition poster" width="207"></a></td>
</tr>
<tr>
<td align="center"><a href="https://zeeekrom.github.io/little-red-sequel/film/">Project film, 3:15</a></td>
<td align="center"><a href="media/poster.jpg">Graduation exhibition poster</a></td>
</tr>
</table>

**Project film:** [watch the 3-minute film](https://zeeekrom.github.io/little-red-sequel/film/)
— 3 min 15 s: the fairy tale the game starts from, what it changes, the branching design, and how one person finished it with an AI art workflow and existing plugins changed and joined into one loop. English narration (synthetic voice) with captions; the pixel windows show real gameplay.

**Gameplay demo:** [watch the full demo](https://zeeekrom.github.io/little-red-sequel/demo/)
— 6 min 35 s of gameplay, MP4. Its music and sound effects are by other creators; most are CC0.

**Poster:** [open the poster](media/poster.jpg)
— the English version of the poster made for the 2024 graduation exhibition. Contact details on the original have been removed.

<img src="media/preview.gif" alt="Gameplay loop: the player leaves the house and crosses the village at night, following the quest tracker" width="560">

A loop from the gameplay demo. The quest "Her" Daily Life sends the player out of the house and across the village at night. The quest tracker in the top left shows the current objective, a waypoint marker shows the distance to it, and examining the drying rack gives a line about the red dress kept there for Little Red Riding Hood.

## Contents

- [At a glance](#at-a-glance)
- [The problem](#the-problem)
- [One scene, start to finish](#one-scene-start-to-finish)
- [The scenes and screens](#the-scenes-and-screens)
- [What the demo contains](#what-the-demo-contains)
- [Design principles](#design-principles)
- [How it was built](#how-it-was-built)
- [Problems that became rules](#problems-that-became-rules)
- [Tools and technology](#tools-and-technology)
- [How it was checked](#how-it-was-checked)
- [What is not finished](#what-is-not-finished)
- [What the project showed](#what-the-project-showed)
- [What carries over to simulation and visualisation](#what-carries-over-to-simulation-and-visualisation)
- [Copyright and terms](#copyright-and-terms)

## At a glance

| | |
|---|---|
| What it is | A narrative RPG demo with exploration, quests and branching dialogue: 2D pixel characters in 3D scenes with pixel-art textures |
| Story | A dark fairy tale that starts bleak and ends hopeful. Themes: refusing a life someone else wrote, thinking for yourself, bullying, living inside a filter bubble |
| Environment | An island and a village built by hand: sculpted terrain, a layer-blended landscape material, baked lighting, height fog, light shafts and Niagara effects |
| AI | Stable Diffusion generated the pixel textures, fitted to the UVs in Photoshop. ChatGPT helped with parts of the C++ header changes, some Blueprint logic and story text. I corrected and integrated everything by hand |
| Engine | Unreal Engine 5.3. Most gameplay logic in Blueprint, with two modified C++ Marketplace plugins and a modified menu asset |
| Team and time | Solo, about three months: two of pre-production, one of assembly |
| Scale | About 199 asset sets (124 3D, 75 2D), three gameplay systems joined into one game, 20 reference games reviewed |
| Status | Playable demo with part of the planned story. Submitted with a thesis in May 2024 |

## The problem

A story-driven RPG needs a written story, scenes built to a plan, a large asset library, and systems for quests, dialogue, menus and saves. This project asked how much of that one person could finish in about three months:

- Which look gives a good trade-off between production speed and quality for one person?
- How can a story with branches and two points of view be planned before any dialogue is written?
- Where can AI tools cover gaps in design, programming and texture work, and what still has to be checked by hand?
- Can existing plugins that were not made to work together be joined into one game?
- Do studio habits, such as requirements, a schedule, version control and technical tests, still help when the team is one person?

The game answers with a 2D-in-3D look, a story chart drawn before the text, an AI-assisted texture pipeline, and three modified Marketplace products joined by my own Blueprints.

## One scene, start to finish

```mermaid
flowchart LR
    M[Concept map in Inkarnate] --> W[White-box in Unreal]
    W --> T[Terrain sculpted and painted from the player's camera]
    T --> X[Material instances tuned]
    A[Finished assets from the asset pipeline] --> X
    X --> L[Lights, fog, effects and post-process]
    L --> B[Lighting baked]
    B --> I[Same pass for each interior]
```

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

## The scenes and screens

| | | |
|---|---|---|
| ![Village stage](media/gallery/01-village-stage.jpg) | ![Campfire](media/gallery/02-campfire.jpg) | ![Market stall](media/gallery/03-market-stall.jpg) |
| ![Village from above](media/gallery/04-village-from-above.jpg) | ![Island overview](media/gallery/05-island-overview.jpg) | ![Rope bridge](media/gallery/06-rope-bridge.jpg) |
| ![Cottage exterior](media/gallery/07-cottage-exterior.jpg) | ![Interior with a light shaft](media/gallery/08-interior-light-shaft.jpg) | ![Interior](media/gallery/09-interior-table.jpg) |

| | | |
|---|---|---|
| ![Village cottage at night](media/screenshots/04-village-cottage.jpg) | ![Village stage](media/screenshots/05-village-stage.jpg) | ![Bridge](media/screenshots/06-bridge.jpg) |
| Village exterior with the quest tracker and a waypoint marker | The village stage, with an interaction prompt | Bridge and river on the way to the signpost |
| ![Home interior](media/screenshots/03-home-interior.jpg) | ![Dialogue at home](media/screenshots/07-dialogue-mother.jpg) | ![Interior dialogue](media/screenshots/08-dialogue-interior.jpg) |
| First quest completed inside the house | Dialogue with Little Red's mother | An interior scene with object dialogue |
| ![Hidden value feedback](media/gameplay/hidden-value-popup.jpg) | ![Quest tracker](media/gameplay/quest-tracker.jpg) | ![Dialogue](media/gameplay/dialogue.jpg) |
| Opening a chest raises a hidden value | Quest tracker with a waypoint and distance | Dialogue with player choices |

Menus are in Chinese and story text is in English. See [What is not finished](#what-is-not-finished).

## What the demo contains

| Part | What is in it |
|---|---|
| Story | Part of the planned story, with dialogue, player choices and story text on loading screens |
| Exploration | Small, dense areas (the village, house interiors) where the player learns by walking around, examining objects and talking to villagers |
| Hidden values | Exploring and talking quietly raise hidden values such as courage; opening a chest is one example |
| Quests | A tracker with the current objective, a waypoint and the distance to it |
| Dialogue | Branching dialogue with player choices, joined to the quest system |
| Interaction | One "walk up and press F" interaction starts dialogue, advances quests, changes scene or adjusts hidden values |
| Player | Movement, saving and loading of position and quest state, and a 2D sprite that switches between standing and walking by velocity |
| Menus and saves | Main menu (continue, new game, load, settings, quit), save and load slots, graphics settings (resolution, window mode, frame rate, quality presets) and audio settings |
| Environment | The island and village: sculpted terrain, a layer-blended landscape material, baked lighting, a sky light, exponential height fog, volumetric light shafts and post-process volumes |
| Materials | Foliage that moves in the wind, masking so objects between the camera and the character do not hide her, UV controls, fresnel, and fades driven by depth and camera distance |
| Effects | Niagara fire, fireflies and smoke; emissive lamps and fire; a startup logo and particle animations made in After Effects and Houdini |
| Assets | About 199 asset sets: roughly 124 3D and 75 2D, plus visual effects, post-processing and character animation |

## Design principles

- **A familiar story with the roles questioned.** Everyone in this world is born holding a fairy-tale book. Most are blank. A few "protagonists" have their whole life written in, and must act it out so the story can be copied into everyone else's book as a lesson. The books say protagonists are always brave and good; some are not, and some of the "villains" never chose the part. Little Red is one of the few who refuses her script. The world itself was built by an AI, and nobody living in it knows that.
- **Two points of view.** After Chapter 0 the player continues as Little Red or as the Big Bad Wolf, who has started to doubt the monster his own book describes. Their storylines cross and reach the same goal, so the same events can be seen from both sides.
- **Branches on what the player did.** Chapters unlock on conditions. Early on, whether Little Red talked to a travelling merchant before the village chief gets to her, and whether a hidden value is above zero, decides between a branch that ends badly and a branch that leads on to the Wolf's village. More generally, when a hidden value crosses a threshold, a different storyline or ending opens.
- **Chart first, text second.** I wrote several complete story proposals (outline, main plot, theme, references) and picked one. Then I drew the whole story as a flowchart with both character lines, chapter names, unlock conditions and a summary of each chapter, and wrote the dialogue and quests from that chart.
- **Guide indirectly.** The early game does not point at the truth. It lets the player notice the gap between what the villagers say and what is in front of them. In places the game breaks the fourth wall and speaks to the player.
- **A look one person can produce.** 2D pixel sprites in 3D environments with pixel textures, in the vein of HD-2D games. I chose it after studying indie games that mix the two, because it balanced production speed and quality for one person.

| | |
|---|---|
| ![The three rules](media/gameplay/three-rules.jpg) | ![Loading screen text](media/gameplay/loading-screen-text.jpg) |
| The village's rules for Little Red, shown at the start | Loading screens carry story text |

A simplified view of the story chart:

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

## How it was built

| Phase | When | What happened |
|---|---|---|
| Pre-production | About two months, 2024 | Research, design documents, technical tests and asset production |
| Assembly and polish | About one month, 2024 | The parts assembled into one game and polished into a packaged build |
| Thesis | May 2024 | Submitted with a thesis written in Chinese; it is not published here |
| Showcase | 9 Oct 2026 | This repository: the demo video, screenshots, production images, poster, and READMEs in English and Chinese |
| Film page | 13–14 Nov 2026 | A web page for the demo video with a terms page, then the 3-minute project film on it |

**Research before design.** I reviewed ten game-jam entries (Ludum Dare, itch.io, Reddit game jams, Global Game Jam) and noted how each was made, what works and what I could borrow; the storytelling and "meta" ideas, and keeping interaction small, came from here. I then reviewed ten games from the Steam indie charts in more depth, which is where the 2D-in-3D look, the non-linear story, multiple endings and two points of view were tested against games that had shipped them. I also kept a table of AI techniques used in game production and studied how one commercial game uses AI features.

| | |
|---|---|
| ![Asset list](media/process/asset-list.jpg) | ![Checking an asset in Blender](media/process/asset-check-blender.jpg) |
| Part of the asset list (in Chinese): name, scene, progress, thumbnail and white-box notes | Checking a finished bridge and its texture in Blender |
| ![Stable Diffusion settings](media/process/sd-webui-settings.jpg) | ![ComfyUI workflow](media/process/comfyui-workflow.jpg) |
| Sampler and upscale settings used for pixel textures (Chinese UI) | A ComfyUI graph tested as an alternative to the WebUI |

<img src="media/process/asset-sheet.jpg" alt="Part of the finished asset library" width="330">

**Assets.** One sheet tracked every asset: Chinese and English name, priority, progress, scene, a thumbnail, the white-box design and the reference. 3D assets started as white-box models in Maya, were unwrapped in RizomUV, got pixel-style textures from Stable Diffusion (two pixel-art LoRAs merged, a pixel-style SDXL base model, img2img), and were fitted to the UVs in Photoshop. This got me to about ten finished assets a day. Props, character sprites and animations were drawn in Aseprite, with the character sprites worked up from reference.

| | | |
|---|---|---|
| ![Foliage and fog materials](media/techart/foliage-and-fog-material.jpg) | ![Landscape blend material](media/techart/landscape-blend-material.jpg) | ![Niagara effects](media/techart/niagara-fireflies-smoke-fire.jpg) |
| Material graphs for wind-driven foliage and fog | Layer-blended landscape material | Niagara effects: fireflies, smoke and fire |

**Programming.** Most gameplay logic is Blueprint. The quest system, the dialogue system and the main menu each started from a different Unreal Marketplace product: a quest plugin (C++ classes with a node-based quest editor, several quest types, completion conditions and an on-screen tracker), a dialogue plugin with a node-based editor for branching dialogue, and a menu asset (new game, continue, load, and graphics and audio settings through Unreal's settings API, with UMG screens). They were not made to work together, so a large part of the programming was modifying them and joining them into one game. I wrote the quests in the quest plugin's editor. The player Blueprint and the interaction Blueprint are my own.

| | | |
|---|---|---|
| ![Interaction Blueprint](media/blueprints/interaction.jpg) | ![Player Blueprint](media/blueprints/player.jpg) | ![Sprite animation state machine](media/blueprints/sprite-animation.jpg) |
| Interaction: entering range shows the prompt and enables input, and pressing the key starts the dialogue | Player Blueprint: movement, and saving and loading position and quest state | Animation Blueprint for the 2D sprite (PaperZD): stand and walk states chosen from velocity |
| ![Main menu](media/screenshots/01-main-menu.jpg) | ![Graphics settings](media/screenshots/02-graphics-settings.jpg) | ![Save and load](media/ui/save-and-load.jpg) |
| Main menu: continue, new game, load, settings, quit | Graphics settings: resolution, window mode, frame rate, quality presets | Save and load slots |

**Running the project.** The documents were audience and gameplay research, story proposals, the non-linear story chart, the asset list and a survey of AI tools used in games. The project was versioned on GitHub every day, with two extra copies on a cloud drive and an SSD. Asset naming rules, the tracking sheet and the habit of testing techniques before committing to them came from my internships at game studios.

## Problems that became rules

| What got in the way | What changed |
|---|---|
| Generated textures did not tile cleanly, and I found no reliable way to fix that | The texture pipeline is used only for pixel art, where seams are hard to see |
| The quest, dialogue and menu products were not made to work together | Each was modified and tried in a small test project before it was joined into the game |
| Some assets did not reach a usable standard in pre-production | They were remade in the second phase, and spare assets were made in advance so a batch that failed review would not hold up the schedule |
| AI output for code and story text was not right as it came | Every result was corrected and integrated by hand |
| Tasks competed for the same time | Design documents came before code, and code before art |

## Tools and technology

- Engine and code: Unreal Engine 5.3 (Blueprint, UMG, Niagara, the PaperZD plugin), Visual Studio 2022
- 3D: Maya 2024, RizomUV, Blender 4.1 (Cycles review renders), Houdini 20
- Textures and materials: Stable Diffusion WebUI, ComfyUI, Photoshop, xNormal, Substance 3D Painter and Designer
- 2D, motion and maps: Aseprite, After Effects, Inkarnate
- Versioning: GitHub, daily

## How it was checked

- Each asset was previewed in Blender's Cycles renderer, named to a convention, and added to the sheet with a screenshot once it passed.
- Each method was tested before I committed to it: the texture pipeline (including a ComfyUI graph tried as an alternative to the WebUI), and the menu, quest and dialogue systems, each built and tried in a small test project before it was moved into the game.
- Each week I checked the time spent per task against the plan and adjusted.

## What is not finished

- This is a demo. Only part of the planned story is playable, and some planned features were cut for time.
- Menus are in Chinese and story text is English only. Language switching was not completed.
- UI art is basic, and some screens and audio are placeholders.
- Known bug: loading a save occasionally hangs on the loading screen.

## What the project showed

- It was the first game I took from a blank page to a packaged build, and it showed me how the parts of production depend on each other.
- Studio habits scale down. Requirements, a schedule, version control and technical tests were as useful for one person as for a team.
- AI tools covered some of my gaps in design and programming and sped up texture work. They did not remove the need to check and fix what they produced.
- I deliberately spent less time on traditional art and more on technical art and programming. That shift is why I went on to study software engineering.

## What carries over to simulation and visualisation

This is a fairy-tale game, but several parts of the work are the same ones a simulation or visualisation scene needs:

- **A place built to match a map.** Map, then white-box, then terrain sculpted to the map, then the finished scene. The order would be the same with a chart or a site plan as the reference.
- **Light and atmosphere decide what can be seen.** Baked lighting, a sky light, exponential height fog, volumetric light shafts and post-process volumes set how far the player can see and what stands out, in night exteriors and lamp-lit interiors.
- **Materials made to be reused.** One layer-blended landscape material, a material instance with exposed controls for every asset, and foliage that moves in the wind.
- **An asset pipeline that is tracked.** About 199 asset sets went through the same steps: naming rules, a tracking sheet and a review render before they entered the engine.
- **Performance settings in the user's hands.** The settings screen exposes resolution, window mode, frame rate and quality presets through Unreal's settings API.
- **Making separate systems work as one.** Two C++ plugins and a menu asset that were not written to work together were modified and joined, and each was tested in a small project first.

## Copyright and terms

© 2024–2026 Little Red: Sequel. All rights reserved; see [LICENSE](LICENSE). Without written permission, nothing in this repository may be copied, republished or adapted, and the project's code and design may not be rebuilt, whether by hand, with automated tools or with AI cloning tools. The code may not be reverse engineered except where the law allows, and the content may not be scraped, bulk-downloaded or used to train or evaluate AI models. Uses the law already allows, such as fair dealing for review or news reporting, are not affected. Sharing links is welcome. The story, the design documents, the environment, the asset library, the materials and effects, and the Blueprint logic that ties the systems together are my own work, with AI assistance where noted. Third-party parts keep their own licence:

- Quest and dialogue systems: two Unreal Marketplace plugins, modified and combined. Main menu, settings and save screens: an Unreal Marketplace asset, modified. These and Unreal Engine are used under Epic Games' licence terms.
- Sprite animation: the PaperZD plugin.
- Texture generation: Stable Diffusion with community pixel-art LoRAs and a pixel-style SDXL base model.
- Music and sound effects in the game and the gameplay demo: by other creators; most are CC0.
- Project film: narration made with Kokoro-82M (Apache 2.0); instrument samples from VSCO 2 Community Edition, the Versilian Community Sample Library and FreePats (CC0); pixel font, text boxes and frames from Lemo-Opuscar (MIT).

Terms, licences and privacy: [terms page](https://zeeekrom.github.io/little-red-sequel/film/terms.html).
Contact: [LinkedIn](https://www.linkedin.com/in/evan-h-165976301/)
