# CrazyGames Release Guide

## Ready-to-upload build

The file `release/mega-tower-defense-crazygames.zip` is the finished HTML5 game package. `index.html` and the `assets` folder are located directly at the root of the ZIP archive. The game loads the official CrazyGames HTML5 SDK v3 and uses only its Rewarded Ad interface. To test outside CrazyGames, extract the ZIP first and serve its directory through a local web server; do not open `index.html` from inside the ZIP viewer.

The build includes 18 individual top-down mission battlefields with roads baked into the artwork, seven original monster classes, 56 distinct tower upgrade appearances, four military vehicle appearances, directional targeting with animated return-to-rest movement, and locally bundled CC0 Kenney sound effects. No network-hosted art or audio files are needed at runtime.

## CrazyGames Portal

1. Sign in at [developer.crazygames.com](https://developer.crazygames.com/) and create a new game.
2. Select **HTML5** as the platform or engine.
3. Upload `release/mega-tower-defense-crazygames.zip` as the game build.
4. Add the title, description, controls, categories, cover image, and preview images requested by the portal.
5. Open the private Preview/Sandbox link and verify these flows:
   - **GET GEMS**: one fully completed ad awards exactly 5 Gems.
   - Cancelled or failed ads award nothing.
   - **Shop → Free Tower**: each completed ad increases the counter exactly once; at 5/5 the player can choose one locked tower.
   - Complete or skip the first-run tutorial.
   - Start, pause, lose, and win a mission.
   - Test the game in desktop and mobile landscape mode.
   - Reload the page and confirm that progress is retained.
6. Submit the build for review after completing the preview test.

Rewarded Ads intentionally work only inside the CrazyGames environment. The ad buttons remain disabled on GitHub Pages and when the game is opened directly on a local machine. Always use the CrazyGames preview to test real ads.

## Store-page information

**Controls**

- **Mouse / touch:** Navigate menus, choose and place towers, select units, upgrade, sell, and change targeting.
- **Start Wave:** Launch the next attack as soon as your defense is ready.
- **Right-click / tap the selected arsenal card again:** Cancel tower placement.
- **1–5:** Select a tower from your current loadout.
- **Space:** Cycle through 1×, 2×, 3×, and 5× battle speed.
- **P:** Pause or resume the battle.

**Description**

Command the ultimate defense across 18 handcrafted battlefields, from crystal forests and frozen rifts to volcanic fortresses and cosmic war zones. Build and upgrade 14 specialized towers, deploy helicopters, strike aircraft, combat vehicles, and siege tanks, then adapt your targeting to stop seven distinct monster classes. Master long-range mortar fire with a close-range blind spot, survive increasingly brutal multi-boss assaults, earn Gems every three cleared waves, unlock new towers and loadout slots, and fight your way to the Final Stand.

**Progress**

Gems, missions, towers, loadout slots, and Free Tower ad progress are stored in the browser. A new player starts with 0 Gems, 0 completed missions, 0/5 Free Tower ads, and the five starter towers.

## Technical ad rules

- An ad starts only after an intentional player click.
- A reward is granted only inside the `adFinished` callback.
- `adError` and cancelled ads do not grant rewards or consume progress.
- Additional input is blocked while an ad is running.
- Loading, gameplay start, and gameplay stop events are reported through the CrazyGames SDK.
- `loadingStop` is sent only after all high-resolution gameplay artwork has loaded.

Official reference: [CrazyGames HTML5 SDK – Advertisement](https://docs.crazygames.com/sdk/html5/advertisement/)

## Quality-guideline audit

- **Fast onboarding:** A new player enters the first mission immediately and receives a four-step visual tutorial covering selection, placement, upgrades, wave controls, speed, and pause.
- **Skippable training:** `SKIP TUTORIAL` is available throughout onboarding; `HOW TO PLAY` can reopen it later.
- **Clear goals and feedback:** The wave target, lives, Gold, Gems, win state, boss alerts, placement range, mortar dead zone, upgrade information, and mission progression are always visible.
- **Consistent controls:** Pointer and touch share the same actions. Keyboard shortcuts use number keys, Space, and P; no browser-sensitive Escape or Ctrl/Cmd shortcuts are required.
- **Responsive layout:** The 16:10 canvas scales to the viewport, supports landscape touch play, and shows a rotate-device prompt in mobile portrait mode.
- **Performance:** Artwork and sounds are local, images use WebP in gameplay, simulation steps are capped, and high game speeds use stable fixed-size update slices.
- **Ads:** Rewarded ads start only from explicit buttons, rewards are granted only by `adFinished`, errors grant nothing, and inputs are blocked while an ad is active.
- **Visual/audio consistency:** All mission, enemy, tower, vehicle, cover, and interface art follows the same fantasy sci-fi style. Bundled sound effects are documented CC0 assets from official Kenney repositories.
- **Submission check still required:** Use the CrazyGames private Preview/Sandbox to verify real ad delivery, SDK events, persistence, audio, and mobile landscape behavior before submission.
