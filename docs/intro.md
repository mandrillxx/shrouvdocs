---
sidebar_position: 1
---

# Getting Started

Let's discover **ShrouvEngine in less than 5 minutes**.

## ShrouvEngine

Get started by **creating a new ShrouvEngine project**.

### What you'll need

- [Node.js](https://nodejs.org/en/download/) version 18.0 or above:
  - When installing Node.js, you are recommended to check all checkboxes related to dependencies.
- [Mantle](https://mantledeploy.vercel.app/) version 0.11.11 or above:
  - When installing Node.js, you are recommended to check all checkboxes related to dependencies.
  - Make sure you setup your authentication, otherwise it will not deploy [Learn more](https://mantledeploy.vercel.app/docs/authentication)

## Generate a new project

Generate a new ShrouvEngine game using the configurable **classic template**.

The classic template will automatically be added to your project after you run the following commands:

```bash
git clone --recursive https://github.com/mandrillxx/shrouvrblx.git
cd shrouvrblx
npm run install
npm run new
```

You can type this command into Command Prompt, Powershell, Terminal, or any other integrated terminal of your code editor.

The command will install all necessary dependencies you need to create an experience.

## Working with your new project

Run the development server:

```bash
# .\shrouvrblx
cd experiences\{projectname}
yarn install
yarn deploy:dev
```

The `yarn deploy:dev` command will build your project, then run your generated `mantle.yml` config which will push it to the roblox site using your provided credentials.
