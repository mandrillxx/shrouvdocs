---
sidebar_position: 1
---

# Entity Component System

**ShrouvEngine** offers the following default systems which integrate with [Matter ECS](https://eryn.io/matter/)

**./client**

- `client/systems/state` - Handles **ClientState** updates and pushes them to slice

**./server**

- `server/systems/replication` - Handles component/entity **replication** between client & server
- `server/systems/renderable` - Handles entity **destruction** and **cleanup**

**./shared**

- `shared/systems/hoverSelection` - Enables entity debug interaction while holding CTRL while in debug mode
- `shared/systems/updateRenderables` - Updates all entity attributes containing **Renderable** component
- `shared/systems/updateTransforms` - Updates all entity transform information containing **Transform** component

It is **not** recommended to change any default systems unless you know what you are doing.

## Create your first System

Create a `.ts` file in any of the following directories:

- `clent/systems/**` - Only replicated to client
- `server/systems/**` - Only replicated to server
- `shared/systems/**` - Replicates to both

```typescript title="Example: client/systems/client.ts"
const player = Players.LocalPlayer;

function client(world: World, state: ClientStore) {
  for (const [id, health] of world.queryChanged(Health)) {
    if (!health.new) return;
    const client = getOrError(
      world,
      id,
      Client,
      "Health component added to non-player entity"
    );
    if (client.player !== player) continue;
    state.setHealth(health.new.current);
  }
}

export = {
  priority: math.huge,
  system: client,
};
```

This system will check for any changed **Health** component on all entities replicated to the client, and if the new state exists, it will send an update to the client state with the new health, which can then update on the GUI.
