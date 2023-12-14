---
sidebar_position: 2
---

# Managing Assets

ShrouvEngine uses [Tarmac](https://github.com/Roblox/tarmac) to efficiently manage all your game assets

Default asset folder structure:

- `assets/badges` - Badge Thumbnail Images
- `assets/images` - In-game Images/Decals
- `assets/lighting` - Lighting assets (e.g. skybox)
- `assets/marketing` - Experience marketing images (e.g. thumbnails, videos, icons)
- `assets/passes` - Game pass marketing content
- `assets/products` - Developer product marketing content
- `assets/sounds` - In-game sounds

## Using your assets

Upload your assets to the respective directory in the `./assets` directory, and simply run the following command in a terminal which will auto-update the game assets in studio

```bash title="./shrouvrblx/experiences/{projectname}"
yarn tarmac
```

## More information

For more information, visit the [Tarmac Documentation](https://github.com/Roblox/tarmac)
