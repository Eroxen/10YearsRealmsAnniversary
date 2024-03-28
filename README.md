# 10YearsRealmsAnniversary
A repository to manage the creation of the datapack for the anniversary map

## How to contribute

If you want to add your mechanics to the map, please follow these steps:

1. Either  
  a) Fork the Repository (faster to set up for you but more complicated down the line if you [want to get the latest changes to the main repository](https://stackoverflow.com/questions/3903817/pull-new-updates-from-original-github-repository-into-forked-github-repository) or [when making a pull request](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request-from-a-fork)).  
  b) Contact Plagiatus on Slack or Discord with your GitHub Username or Email to request access to the repository and then [create a new branch](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-and-deleting-branches-within-your-repository) to work on.  
2. Make your changes **according to the Guidelines** below
3. Open a Pull Request in which you state  
   a) What area / building / minigame (include coordinates) is this mechanic for?  
   > e.g. "Lookout Tower, Elytra Minigame, 120 50 42"  

   b) What does it aim to implement? Rather be too specific than too vague. Make a list if it's a lot.  
    > e.g. "Adds ash particles to the booth for cool effects."

   c) If you're giving out currency, how much and for what?

   d) What namespace did you use?

   e) Is this an update or a new thing?

   f) Please confirm that you've read and to the best of your knowledge adhered to the guidelines.
4. Reviewers will have a look at your code and possibly request changes. With enough approvals, your code will be added to the datapack.

## Guidelines 

### Datapack

1. **Namespace everything.** Choose a name for your datapack folder and a prefix for everything else (tags, scoreboards, etc). **Do not use other namespaces than your own!** _(Exception: The shared namespaces, see below)_
2. **Only run as much as is needed.** Ensure your code only runs when it's needed (e.g. minigame code only needs to run while someone is playing the minigame). Also in this category: if something can get away with being run slower than 20 times a second, run it slower (there are utilities available for this).
3. **Only affect your own entities.** Meaning you should always tag your entities and always limit your commands to your own entities. Players that are in your area count as your entities.
4. **Don't /clear without any arguments.** Similarly, don't try to control players inventories. If they need to have an empty inventory for your game, let them manually empty their inventory into a chest or something and prevent them from entering until they've done so.
5. **Keep it multiplayer friendly.** Don't assume your code is the only code running at any time. Ensure players can play a minigame without affecting anyone else.
6. **Setup all relevant objectives inside your namespaces `load` function** and add it to the shared load.json file.
7. **Keep things readable and reviewable.** Don't actively try to obscure your code. Mabye add a few comments so it's easier for reviewers (and yourself) to follow along.
8. **Do not use global single-use things like gamerules or the worldborder**. To avoid any conflicts with these things, do not change gamerules, the time, the worldborder or anything else that is global only and cannot be prefixed. If in doubt, better to make an issue and ask whether you can do something.
9. **Optimize reasonably.** Take some precautions on making optimized code to prevent lag from your mechanics. We don't expect perfect performance, but simple rules such as keeping your NBT checks to a minimum or using @s wherever possible are a good start. Resources: [MinecraftCommands Guide](https://www.reddit.com/r/MinecraftCommands/wiki/optimising/), [Neylz Guide](https://github.com/neylz/opti-mcfunction)
10. **PRs should be self-contained.** Changes in one Pull Request should be self-contained and only implement one connected mechanic. For example, only include a single minigame or booth mechanics in one PR, not both.

### Resourcepack

1. **Don't modify anything vanilla: blocks, items, entities, particles, GUIs or anything else.**
2. **Only modify items through custom model data.** To avoid custom model data overlaps, please follow the numbering convention of https://mcdatapack.vercel.app to avoid conflicts.
3. You **may use custom fonts**. Do not modify the default files.
4. You **may use custom translations.** Your translation keys need to start with your chosen namespace.
5. When adding new textures and models, use your namespace as the root folder, don't change anything inside the minecraft folder except for model files to include your custom model data. Include your files in a way that doesn't require an atlas, e.g. `namespace:item/example/my_item` instead of `namespace:example/my_item`.
6. For the sake of keeping the RP lean: **No custom music**. Short soundsnippets are okay, but make sure to compress them to reasonable sizes. Preferably use built-in sounds.
7. Keep your texture sizes to powers of 2 as to not mess up the mipmap level. Also keep them to a reasonable size.
8. No shaders.

These are general guidelines. Exceptions may be made on a case by case basis.

## Namespaces

Add the namespaces you used in here when you make a pull request. **Namespaces labeled by "everyone" are shared. You can use them for their purpose at will.**

|Folder|Prefix|User|Usecase
|-|-|-|-|
|utilities|util|everyone|Reusable functions that provide some sort of utility.
|trophies|trophy|everyone|Mechanics for a world-wide trophy / achievements system.

## Utilities

If you have a utility added that can be reused, please (briefly) explain it here.

### slower clocks by Plagiatus
If you need something run continously but slower than 20 times a second, there are some function tags available that run slower. Their names include how slow they run (e.g. 10t means once every 10 ticks).

 - `#utilities:slow_clock/2t`
 - `#utilities:slow_clock/5t`
 - `#utilities:slow_clock/10t`
 - `#utilities:slow_clock/1s`
 - `#utilities:slow_clock/2s`
 - `#utilities:slow_clock/60s`

## Shared Things

### Objectives

The `currency` dummy objective denotes a players current currency. You can give out reasonable amounts for winning games or completing other tasks. Think of 100 currency as a reward for the perfect, hardest achievement and adjust your rewards based on that.
