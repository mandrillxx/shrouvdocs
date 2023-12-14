---
sidebar_position: 2
---

# Updating

This section assumes you have correctly installed and setup **ShrouvEngine** using the provided documentation.

ShrouvEngine has **much more to offer**, and frequently receives updates!

## Updating shrouvrblx

ShrouvRBLX is the main repository containing all submodules

To quickly update all ShrouvEngine components:

```bash
cd shrouvrblx
git fetch
git pull
git submodule update --remote
```

After completing those steps, ShrouvEngine and its components should all be **up-to-date** with the latest changes.

## Contributing to the engine

ShrouvEngine is accessible to modify as you please. Once you have modified `.\shrouvrblx\engine` to your liking, follow these steps:

```bash
# .\shrouvrblx
npm run build
```

And then in your ShrouvEngine experience

```bash
# .\shrouvrblx\experiences\experiencename
npm i ..\..\engine\rbxts-shrouvengine-1.0.0.tgz
```
