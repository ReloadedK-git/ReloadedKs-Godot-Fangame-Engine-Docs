# Engine features

This section will mention some of this engine's features, in no particular order:

1. Is meant to be modified with relative ease.
2. Designed to reduce coupling as much as possible, other than using dedicated autoloads.
3. Includes several menus, namely:
    1. Main menu (3 save slots, loading, erasing).
    2. Settings menu (Music volume, sound volume, fullscreen, vsync, auto-resetting, reset to defaults, controls menu, back).
    3. Controls menu (allows input remapping, both for keyboards and controllers).
4. Includes most of the classic fangame engine gimmicks (vines, triggers, water, jump refreshers, etc), while also adding some new ones.
5. Includes sloppes.
6. Native controller support.
7. Accessibility settings (multiple input methods, input remapping, easy to understand designs for menus, text updates according to the current input method).
8. Supports save and settings encryption. Encryption can use a string password or a unique ID.
9. Saves are encrypted by default, and made both small and easy to modify which works well for things like collectables/items.
10. Global settings unencrypted by default and can be modified externally, if so desired.
11. Mute/unmute music with Ctrl+M, similar to other fangame engines.
12. Includes a "god mode", which can be toggled by holding Ctrl and pressing D. This mode will make the player invincible, teleport it to the mouse on right click, and show some extra information on the top-right corner of the window.
13. Facilitates repetitive tasks as much as possible and avoids hardcoding things like music thanks to Godot's exported variables.
14. Certain objects show extra visual feedback on the editor, for ease of use.
15. Basic warp transitions.
16. The ESC key only quits the game on the main menu. While playing, it opens the pause menu.
17. The music and sound volume can be changed directly from the pause menu. Also allows for returning to the main menu or resuming the game, which is more intuitive.
18. Has a default "dummy enemy", which can be edited easily to suit your needs.
19. Has a global class which defines the type of weapon/attack/proyectile the player uses, making things like multiple weapons, power-ups or attacks types easier to implement.
20. Easy to use and modify backgrounds types (Color, texture, scrolling, specific).
21. (Very) easy collectable system.
22. Includes its own dialog system. Recommended for simpler games, as it does not support localization or external translation files.
23. The player object was designed to be modular and easy to edit.
24. Multiple camera types (fixed, dynamic), with zoom support and a few other things.
25. (Very) simple to use music system, with non-repeating music and user defined looping points.
26. Save points will save when hit with bullets or by pressing the "shoot" button while the player is colliding with it.
27. Single difficulty setting (having multiple "difficulties" erase certain saves felt a little dated, personally).
28. Warps can teleport the player to its spawn point or to a previously defined point, with warp transitions.
29. Global HUD object, for showing information on top of the screen. Currently used to show extra information when "god mode" is toggled.
30. Tilemaps divided by size (16x16, 32x32).
31. Simple to use trigger system and triggerable objects.
32. Global sound manager, which manages multiple sounds and won't cut them if an object is freed/destroyed.
33. Clean folder and resource structure.
34. Smaller details and systems not mentioned here.

---

**Previous page: [01. Introduction](01_introduction.md)**

**Next page: [03. Project Structure](03_project_structure.md)**
