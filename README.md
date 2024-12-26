# Astro Template: Space

**Space** is an opinionated Astro starter template with built-in support for Tailwind CSS, Prettier, view transitions, and import aliases.

Using `bunx create-astro@latest` or `npm create astro@latest` provides everything you need to create a basic Astro application. However, it is missing a few useful items that I found myself manually adding to every Astro project I created.  To address this problem, I created this template to automatically include these items. Additionally, a custom PowerShell function was created to deploy this template and provide some additional functionality that the template cannot.

The template includes:
- [Tailwind CSS (v3)](https://tailwindcss.com/)
- [Prettier](https://prettier.io/)
- Astro [View Transitions](https://docs.astro.build/en/guides/view-transitions/)
- Astro [Import Aliases](https://docs.astro.build/en/guides/typescript/#import-aliases)
- A default `MainLayout.astro` layout file
- A default `global.css` file
- Default `.vscode` files to properly handle Tailwind CSS, recommended extensions, and default Prettier formatters
- A blank `index.astro` page

The PowerShell function:
- Creates additional empty folders: `Assets` and `Components`
- Blanks out the `README.md` file
- Runs `astro update` to update the core Astro packages to the latest versions and your preferred package manager (npm or bun) to update the other packages
- Runs the `prettier` CLI to provide an intial format of all project files
- Automatically navigates to the project folder and peforms an initial install
- Provides an option to launch the site post deployment and/or launch the project folder with VS Code

## Deployment Methods
> Note:  
> At this time using `bun create` is dependent on `npm` being present in the path.  
> It is recommended to install `Node.js` even if `bun` is used exclusively.
### bun
```sh
bun create astro@latest -- --template smart-ace-designs/astro-space project-name
```
### npm
```sh
npm create astro@latest -- --template smart-ace-designs/astro-space project-name
```
### PowerShell
Add this function to your PowerShell profile or a PowerShell module:
```powershell
function New-AstroSpaceProject
{
    [CmdletBinding()]
    Param
    (
        [Parameter(Mandatory = $true)] [string]$ProjectName,
        [Parameter(Mandatory = $true)] [string]$Location,
        [Parameter(Mandatory = $false)] [switch]$StartCode,
        [Parameter(Mandatory = $false)] [switch]$StartApp,
        [Parameter(Mandatory = $false)] [ValidateSet("bun", "npm")] [string]$PackageManager = "bun"
    )

    switch ($PackageManager)
    {
        "bun" {$PackageManagerX = "bunx"}
        "npm" {$PackageManagerX = "npx"}
    }

    Clear-Host
    $Message = "Astro Deployment Tool"
    $Width = $Host.UI.RawUI.WindowSize.Width
    Write-Host
    Write-Host ((" " * ($Width - $Message.Length)) + $Message) -ForegroundColor Green
    Write-Host ("=" * $Width)

    if (Test-Path -Path "$Location\$ProjectName")
    {
        Write-Host "`nProject folder ($ProjectName) already exists."
        Write-Host "Operation cancelled...liftoff failed!"
        return
    }

    Set-Location $Location
    & $PackageManagerX create-astro@latest -- --template smart-ace-designs/astro-space `
        --git --no-install $ProjectName

    if (!(Test-Path -Path $ProjectName))
    {
        Write-Host "`nProject folder ($ProjectName) was not created."
        Write-Host "Operation cancelled...liftoff failed!"
        Write-Host "`nIf using Bun please run `"bun pm cache rm`" to clear the cache and try again."
        return
    }
    
    Write-Host
    Set-Location $ProjectName
    switch ($PackageManager)
    {
        "bun" {& $PackageManager install --no-summary}
        "npm" {& $PackageManager install --silent}
    }

    & $PackageManagerX @astrojs/upgrade
    & $PackageManager update --silent --save

    [void](New-Item -Name "assets" -Path src -ItemType Directory)
    [void](New-Item -Name "components" -Path src -ItemType Directory)
    Clear-Content -Path "README.md"

    Write-Host
    & $PackageManagerX prettier . --write --log-level silent
    & $PackageManagerX prettier . --check
    if ($StartCode -and (Get-Command code -ErrorAction SilentlyContinue)) {code .}
    Write-Host
    Write-Host ("=" * $Width)
    if ($StartApp) {& $PackageManager run dev}
}
```
https://github.com/user-attachments/assets/1d6ac9dd-67ac-4849-9c07-5cd07ef84ec1

## Project Structure

Inside of your Astro project you will see the following folders and files:

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
├── .gitignore
├── .prettierrc.mjs
├── astro.config.mjs
├── package.json
├── README.md
├── tailwind.config.mjs
└── tsconfig.json
```

