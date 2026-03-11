<!-- ASTRO:REMOVE:START -->

# Astro Template: Space

Astro **Space** is an opinionated Astro 6 starter template with built-in support for Tailwind CSS, Prettier, view transitions, and aliases.

Using `create astro@latest` provides everything you need to create a basic Astro 6 application. However, it is missing a few useful items that you might find yourself manually adding to every new Astro 6 project. The **Space** template was created to automatically include these items. This provides a great starting point for a new Astro 6 project with Tailwind.

The template includes:

- An initial Astro 6 project structure
- Astro [View Transitions](https://docs.astro.build/en/guides/view-transitions/)
- Astro [Aliases](https://docs.astro.build/en/guides/imports/#aliases)
- [Tailwind CSS v4.2](https://tailwindcss.com/)
- [Prettier](https://prettier.io/)
- A default _MainLayout.astro_ layout file
- A default _global.css_ file
- Default _.vscode_ files to properly handle Tailwind CSS, recommended extensions, and default Prettier formatters
- A blank _index.astro_ page
- The `dev` script set to `"astro dev --open"`

An optional [PowerShell function](https://github.com/Smart-Ace-Designs/SmartAceDesigns.AstroLiftoff) (standalone or as part of a PowerShell module) is available to deploy the above template and provide the following additional functionality:

- Creates additional empty folders: _assets_ and _components_
- Runs the `prettier` CLI to provide an intial format of all project files
- Initializes a _Git_ repository
- Automatically navigates to the project folder and peforms an initial install
- Runs `astro update` to update the core Astro packages to the latest versions and runs your preferred package manager (npm or bun) to update the other packages
- Provides an option to launch the site and/or open the project folder with VS Code post deployment

## Deployment Methods

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

### PowerShell

The optional PowerShell function and module are available here:
[SmartAceDesigns.AstroLiftoff](https://github.com/Smart-Ace-Designs/SmartAceDesigns.AstroLiftoff)

```sh
New-AstroProject -ProjectName project-name -Location parent-directory -Template astro-space
```

https://github.com/user-attachments/assets/2f64b212-4590-4809-b232-f8d748c19ab6

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
│   ├── styles/
│   │   └── global.css
│   └── content.config.ts
├── .gitignore
├── .prettierignore
├── .prettierrc.mjs
├── astro.config.mjs
├── package.json
├── README.md
└── tsconfig.json
```

The optional `New-AstroProject` PowerShell function will add these additional directories to your project root:

```text
/
└── src/
    ├── assets/
    └── components/
```

<!-- ASTRO:REMOVE:END -->
