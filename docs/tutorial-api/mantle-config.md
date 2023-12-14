---
sidebar_position: 1
---

# Mantle Config

ShrouvEngine uses [Mantle](https://mantledeploy.vercel.app/) under the hood to manage game information

- You can view the [Configuration Reference](https://mantledeploy.vercel.app/docs/configuration/reference) to see direct API references, however ShrouvEngine uses its own declarations based off the Mantle API

# API Reference

Below is the **ShrouvEngine API** for the **Mantle Configuration**

```typescript
interface MantleEnvironment {
  label: string;
  branches?: string[];
  tagCommit?: boolean;
  targetNamePrefix?: "environmentLabel" | object;
  targetAccess?: "public" | "private" | "friends";
  targetOverrides?: MantleExperience;
}
```

```typescript
export type Genre =
  | "all"
  | "adventure"
  | "building"
  | "comedy"
  | "fighting"
  | "fps"
  | "horror"
  | "medieval"
  | "military"
  | "naval"
  | "rpg"
  | "sciFi"
  | "sports"
  | "townAndCity"
  | "western";
```

```typescript
interface MantleExperienceConfiguration {
  genre?: Genre;
  playableDevices?: Array<"computer" | "phone" | "tablet" | "console" | "vr">;
  playability?: "public" | "private" | "friends";
  paidAccess?: "disabled" | { price: number };
  privateServers?: "disabled" | "free" | { price: number };
  enableStudioAccessToApis?: boolean;
  allowThirdPartySales?: boolean;
  allowThirdPartyTeleports?: boolean;
  avatarType?: "r6" | "r15" | "playerChoice";
  avatarAnimationType?: "standard" | "playerChoice";
  avatarCollisionType?: "outerBox" | "innerBox";
}
```

```typescript
interface DeveloperProduct {
  name: string;
  description?: string;
  icon?: string;
  price: number;
}
```

```typescript
interface GamePass {
  name: string;
  description?: string;
  icon: string;
  price?: number;
}
```

```typescript
interface Badge {
  name: string;
  description?: string;
  icon: string;
  enabled?: boolean;
}
```

```typescript
interface MantlePlaceConfiguration {
  name?: string;
  description?: string;
  maxPlayerCount?: number;
  allowCopying?: boolean;
  serverFill?: "robloxOptimized" | "maximum" | { reservedSlots: number };
}
```

```typescript
interface MantlePlace {
  file: string;
  configuration: MantlePlaceConfiguration;
}
```

```typescript
interface MantleExperience {
  configuration?: MantleExperienceConfiguration;
  places?: { [key: string]: MantlePlace };
  icon?: string;
  thumbnails?: string[];
  socialLinks?: { title: string; url: string }[];
  products?: { [key: string]: DeveloperProduct };
  passes?: { [key: string]: GamePass };
  badges?: { [key: string]: Badge };
  assets?: Array<string | { file: string; name: string }>;
  spatialVoice?: { enabled: boolean };
  notifications?: { [key: string]: { name?: string; content: string } };
  state?:
    | "local"
    | { localKey: string }
    | { remote: { region: string; bucket: string; key: string } };
}
```

```typescript
interface MantleTarget {
  experience: MantleExperience;
}
```

```typescript
interface MantleConfig {
  owner?: "personal" | { group: number };
  payments?: "owner" | "personal" | "group";
  environments: MantleEnvironment[];
  target: MantleTarget;
}
```

# Using the API

**ShrouvEngine CLI** uses the following process to update the `mantle.yml` configuration:

1. Take a default template with the **MantleConfig** interface
2. Interchange the CLI inputted values
3. Convert the JSON with the updates values into YAML
4. Output into generated `mantle.yml` config

### Note

The current CLI does not take into account all configuration values, so it's recommended to update the config file after it's been generated.

Alternatively, you can select the **full** config option instead of **easy** selection.
