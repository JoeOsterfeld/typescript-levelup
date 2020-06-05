# Steps

## Startup commands
1. `mkdir typescript-starter`
1. `cd typescript-starter/`
1. `npm i -g @nrwl/cli`
1. `npx create-nx-workspace@latest pets`
    - Choose empty project
    - Use the NX Cli
1. `cd pets`
1. `npm i -D @nrwl/angular @nrwl/express concurrently`
1. `npm i cors`
1. `nx generate @nrwl/angular:app petsFrontEnd`
1. `nx generate @nrwl/express:app petsFrontEnd`
1. `nx generate @nrwl/node:library classes`
1. package.json, add script
```json
    "serve-all": "concurrently \"nx serve pets-front-end\" \"nx serve pets-back-end\""
```
1. New terminal window `npm run serve-all`


## Classes Lib
1. Add classes code

## Front end
1. Add `.scss` code in `styles.scss`
1. `nx g interceptor http/petsHttp --project pets-front-end`
1. Go into interceptor and add code
1. Go to app.moule and add provider code
1. Add `app.component.html` and `app.component.ts`

## Back end
1. Use cors
1. Add middleware.ts file in app
1. Add post request code
1. Add get request code