# Astro Template: Space

An opinionated blank Astro template with built-in support for Tailwind CSS, Prettier, view transitions, and import aliases.

```sh
npm create astro@latest -- --template smart-ace-designs/astro-space project-name
```

```powershell
# Example PowerShell function to provide more granular control of deploying a new Astro project with this template using bun or npm.
# Add to your PowerShell profile or custom PowerShell module.

function New-AstroProject
{
    [CmdletBinding()]
    Param
    (
        [Parameter(Mandatory = $true)] [string]$ProjectName,
        [Parameter(Mandatory = $true)] [string]$Location,
        [Parameter(Mandatory = $false)] [switch]$StartCode,
        [Parameter(Mandatory = $false)] [switch]$StartApp,
        [Parameter(Mandatory = $false)] [ValidateSet("bun", "npm")] [string]$PackageManager = "bun",
    )

    switch ($PackageManager)
    {
        "bun" {$PMX = "bunx"}
        "npm" {$PMX = "npx"}
    }

    Clear-Host
    $Message = "Astro Deployment Tool"
    $Width = $Host.UI.RawUI.WindowSize.Width
    Write-Host
    Write-Host ((" " * ($Width - $Message.Length)) + $Message) -ForegroundColor Green
    Write-Host ("=" * $Width)
    if (!(Test-Path -Path "$Location\$ProjectName"))
    {
        Set-Location $Location
        & $PMX create-astro@latest -- --template smart-ace-designs/astro-major-tom --typescript strict --no-install --no-git $ProjectName

        if (Test-Path -Path $ProjectName)
        {
            Set-Location $ProjectName
            [void](New-Item -Name "components" -Path src -ItemType Directory)
            [void](New-Item -Name "assets" -Path src -ItemType Directory)
            Write-Host
            switch ($PackageManager)
            {
                "bun" {& $PackageManager install --no-summary}
                "npm" {& $PackageManager install --silent}
            }
            & $PMX @astrojs/upgrade
            & $PackageManager update tailwindcss prettier prettier-plugin-astro prettier-plugin-tailwindcss --silent
            Write-Host
            & $PMX prettier . --write --log-level silent
            & $PMX prettier . --check
            if ($StartCode -and (Get-Command code -ErrorAction SilentlyContinue)) {code .}
            Write-Host
            Write-Host ("=" * $Width)
            if ($StartApp) {& $PackageManager run dev}
        }
        else
        {
            Write-Host "`nProject folder ($ProjectName) was not created.`nOperation cancelled...liftoff failed!"
            Write-Host "`n`nIf using Bun, please run `"bun pm cache rm`" to clear the bunx cache and then try again."
        }
    }
    else
    {
        Write-Host "`nProject folder ($ProjectName) already exists.`nOperation cancelled...liftoff failed!"
    }
}
```

## Project Structure

Inside of your Astro project, you'll see the following folders and files:

```text
/
├── .vscode/
│       └── extensions.json
│       └── launch.json
│       └── settings.json
├── public/
│       └── favicon.svg
├── src/
|   ├── layouts/
│       └── MainLayout.astro
│   ├── pages/
│       └── index.astro
|   ├── styles/
│       └── styles.css
|   └── env.d.ts
├── .gitignore
├── .prettierrc.mjs
├── astro.config.mjs
├── package.json
├── README.md
├── tailwind.config.mjs
└── tsconfig.json
```

Astro looks for `.astro` or `.md` files in the `src/pages/` directory. Each page is exposed as a route based on its file name.

Astro/React/Vue/Svelte/Preact components are put in `src/components/` by convention.

Any static assets, like images, can be placed in the `public/` directory.

## Commands

All commands are run from the root of the project, from a terminal:

| Command                   | Action                                           |
| :------------------------ | :----------------------------------------------- |
| `npm install`             | Installs dependencies                            |
| `npm run dev`             | Starts local dev server at `localhost:4321`      |
| `npm run build`           | Build your production site to `./dist/`          |
| `npm run preview`         | Preview your build locally, before deploying     |
| `npm run astro ...`       | Run CLI commands like `astro add`, `astro check` |
| `npm run astro -- --help` | Get help using the Astro CLI                     |

## Additional Information

Please check the official [Astro documentation](https://docs.astro.build) or jump into the official [Astro Discord server](https://astro.build/chat).
