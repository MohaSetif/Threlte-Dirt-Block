# create-threlte

Everything you need to build a Svelte project, powered by [`create-svelte`](https://github.com/sveltejs/kit/tree/master/packages/create-svelte).

## Creating a project

If you're seeing this, you've probably already done this step. Congrats!

```bash
# create a new project:
npm create threlte my-project
```

## Developing

Once you've created a project and installed dependencies with `npm install` (or `pnpm install` or `yarn`), start a development server:

```bash
npm run dev

# or start the server and open the app in a new browser tab
npm run dev -- --open
```

## The Threlte packages:

@threlte/core:
Compose three.js scenes declaratively and state-driven. Three.js and Threlte's core the library are required.


@threlte/extras:
Components, helpers, hooks and more that extend the core functionality.


@threlte/gltf:
A command-line tool that turns GLTF assets into declarative and re-usable Threlte components. The generated Threlte components make use of the package @threlte/extras.


@threlte/rapier:
Components and hooks to use the Rapier physics engine in Threlte.


@threlte/theatre:
Components and hooks to use the animation library Theatre.js in Threlte.


@threlte/xr:
Components and hooks for VR and AR.


@types/three:
TypeScript types for three.js.

Install the packages with npm, pnpm, yarn or any other package manager you prefer.
```
npm install three @threlte/core

```

You can preview the production build with `npm run preview`.

> To deploy your app, you may need to install an [adapter](https://kit.svelte.dev/docs/adapters) for your target environment.
> To learn more about Threlte, check this documentation website: https://threlte.xyz/
