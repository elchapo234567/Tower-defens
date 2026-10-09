# CrazyGames Release Guide

## Ready-to-upload build

The file `release/mega-tower-defense-crazygames.zip` is the finished HTML5 game package. `index.html` and the `assets` folder are located directly at the root of the ZIP archive. The game loads the official CrazyGames HTML5 SDK v3 and uses only its Rewarded Ad interface.

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

- Mouse / touch: use menus, place towers, select towers, upgrade, sell, and change targeting
- Start Wave button: launch the next attack immediately when your defense is ready
- Right click or tap the selected arsenal card again: cancel tower placement
- Number keys 1–5: select a tower from the arsenal
- Spacebar: cycle through 1×, 2×, 3×, and 5× game speed
- P: pause or resume the battle

**Description**

Build the ultimate defense across lush floating islands, frozen rifts, and volcanic strongholds. Choose your loadout, place and upgrade 14 specialized high-detail towers, deploy helicopters, aircraft, and military vehicles, then adapt their targeting to survive 18 increasingly brutal missions. Start each assault when your defense is ready, earn Gems every three cleared waves, defeat multi-boss attacks, unlock new towers and loadout slots, and master every battlefield on your way to the Final Stand.

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
