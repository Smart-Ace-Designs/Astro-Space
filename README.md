<!-- ASTRO:REMOVE:START -->

# Astro Template: Space

Astro **Space** is an opinionated [Astro 7](https://astro.build/) starter template with built-in support for Tailwind CSS, Prettier, view transitions, and aliases.

Using `create astro@latest` provides everything you need to create a basic Astro 7 application. However, it is missing a few useful items that you might find yourself manually adding to every new Astro 7 project. The **Space** template was created to automatically include these items. This provides a great starting point for a new Astro 7 project with Tailwind.

The template includes:

- An initial Astro 7 project structure
- Astro [View Transitions](https://docs.astro.build/en/guides/view-transitions/)
- Astro [Aliases](https://docs.astro.build/en/guides/imports/#aliases)
- [Tailwind CSS](https://tailwindcss.com/)
- [Prettier](https://prettier.io/)
- A default _MainLayout.astro_ layout file
- A default _global.css_ file
- Default _.vscode_ files to properly handle Tailwind CSS, recommended extensions, and default Prettier formatters
- A blank _index.astro_ page
- The `dev` script set to `"astro dev --open"`

## Deployment Methods

>[!note]
>The `AGENTS.md` and `CLAUDE.md` files will be created automatically by the `create astro@latest` npm initializer. Use the `--no-ai` flag to opt out of creating these files.

### npm

```sh
npm create astro@latest -- --template smart-ace-designs/astro-space project-name
```

### bun

```sh
bun create astro@latest -- --template smart-ace-designs/astro-space project-name
```

### pnpm

```sh
pnpm create astro@latest --template smart-ace-designs/astro-space project-name
```

### yarn

```sh
yarn create astro@latest --template smart-ace-designs/astro-space project-name
```

## Project Structure

After deploying the Astro **Space** template you will see the following files and directories in your project root:

```text
/
├── .vscode/
│   ├── extensions.json
│   ├── launch.json
│   └── settings.json
├── public/
│   ├── favicon.ico
│   └── favicon.svg
├── src/
│   ├── layouts/
│   │   └── MainLayout.astro
│   ├── pages/
│   │   └── index.astro
│   └── styles/
│       └── global.css
├── .gitignore
├── .prettierignore
├── .prettierrc.mjs
├── AGENTS.md
├── astro.config.mjs
├── CLAUDE.md
├── package.json
├── README.md
└── tsconfig.json
```

<!-- ASTRO:REMOVE:END -->
