# [HW] Library — compatibility patches

XML patches that make RimWorld mods work together, used by **[HW] Library Gate** together with
**[HW] Auto Patches**. When a player has every mod a patch is for, the game offers to install it.

## Layout

```
patches/<id>/patch.xml       the patch
patches/<id>/patch.json      what it is for
index.json, index.json.sig   generated and signed by the maintainer, do not edit
```

`patch.json`:

```json
{
  "mods": ["author.mod-a", "author.mod-b|author.mod-b-alt"],
  "game": ["1.6", "1.7"],
  "author": "YourName",
  "version": "1",
  "title": { "English": "Short title", "Russian": "Короткое название" },
  "text":  { "English": "What it fixes.", "Russian": "Что исправляет." }
}
```

Every entry of `mods` must be active (`a|b` means either of them). `game` limits game versions (empty = all).

## Rules

Only the game's own patch operations are allowed:
`PatchOperationAdd`, `Insert`, `Remove`, `Replace`, `AttributeAdd`, `AttributeSet`, `AttributeRemove`,
`AddModExtension`, `SetName`, `Sequence`, `Test`, `Conditional`, `FindMod`.

No classes from other mods (they would run their own code), no DTD, no DLLs, at most 512 KB and 2000 operations.
The game checks this again before applying a patch. Library patches are applied after all mods' own patches.

## Sending a patch

Open an issue with the **submission** label and attach `patch.xml` and `patch.json`. You need a GitHub account.

`index.json` is signed with the maintainer's key, so the game rejects any file that was changed by anyone else.
