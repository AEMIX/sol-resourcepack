# Sol — resource pack

The client resource pack for the Sol Minecraft server. **This repository is public only so the
server can serve the pack**; the game itself lives elsewhere and is private.

The download URL the server uses:

```
https://raw.githubusercontent.com/AEMIX/sol-resourcepack/main/sol-resourcepack.zip
```

## What it does

Blanks the vanilla HUD elements Sol does not use, by replacing their sprites with transparent
images of the same size:

| Hidden | Why |
|---|---|
| Hunger bar | Sol has no food economy. Hunger is pinned server-side and never moves. |
| Armour row | Vanilla armour points are suppressed on purpose — `Stat.DEFENSE` is the only mitigation there is — so the row was showing a number that does nothing. |
| XP bar | Sol's Level track is not vanilla XP, and two progress bars disagreeing on screen is worse than one being absent. |

**Hearts are deliberately left alone.** The server scales the display to ten hearts whatever the
real health pool is, so they read as a health bar rather than a wall of icons, and the exact figure
sits in the action bar beside them.

## Changing it

Do not hand-edit `sol-resourcepack.zip` — it is a build output. In the main repo:

```
java tools/MakeResourcePack.java   # regenerate the blank sprites
./gradlew resourcePack             # rebuild the zip and print its SHA-1
./tools/publish-resourcepack.ps1   # copy it here, commit, push
```

The server computes the pack's SHA-1 from the copy bundled in its own jar, so there is no hash to
keep in sync by hand — but the file published here **must** be the one that build produced, or
clients will download a pack whose hash does not match and silently discard it. That is what the
publish script is for.

The zip is built reproducibly (no timestamps, fixed file order), so an unchanged pack always
produces the same bytes and the same hash.
