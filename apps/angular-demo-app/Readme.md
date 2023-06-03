# Setup of angular universal in Nx workspace

# Setup Angular CLI 

1. Add a file `angular.json` to your root directory and paste the following content:

```json
{
  "$schema": "./node_modules/@angular/cli/lib/config/schema.json",
  "cli": {
    "analytics": false
  },
  "version": 1,
  "newProjectRoot": "[NX_APPS_FOLDER]",
  "projects": {
    "[NX_PROJECT_FOLDER]": {
      "projectType": "application",
      "root": "[NX_APPS_FOLDER]/[NX_PROJECT_FOLDER]",
      "architect": {
        "build": {
          "executor": "@angular-devkit/build-angular:browser",
          "outputs": ["{options.outputPath}"],
          "options": {
            "main": "[NX_APPS_FOLDER]/[NX_PROJECT_FOLDER]/src/main.ts",
            "tsConfig": "[NX_APPS_FOLDER]/[NX_PROJECT_FOLDER]/tsconfig.app.json",
            "outputPath": "dist/[NX_PROJECT_FOLDER]/browser"
          }
        }
      }
    }
  }
}
```

- NX_APPS_FOLDER - normally "apps"
- NX_PROJECT_FOLDER - your project folder e.g. apps/my-app

2. Add the folowing script to your workspace `package.json` to have a shorthand for the Angular CLI:

```json
{
  "scripts": {
    "ng": "npx @angular/cli"
  }
}
```

3. Execute the ng generate command `npm run ng -- add @nguniversal/express-engine`

4. Rename `angular.json` to `_angular.json` or delete it to avoid interference with Nx

5. Copy the following settings `server`, `serve-ssr`, `prerender` from `architect` in `angular.json` into your `project.json` of the target project. e.g. `app/my-app/project.json`
6. In your `project.json` change `builder` to `executor` to align with the Nx schema.
7. Copy the `outputPath` from the `architect.build` in `angular.json` and adopt your `project.json` with the new value
