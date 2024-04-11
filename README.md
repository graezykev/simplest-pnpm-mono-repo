# Simplest Mono Repo With pnpm

## init a mono repo

- `mkdir my-mono-repo`

- `pnpm init`

## declare workspace directory

assuming you (are going to) have

  - `packages/p1`
  - `packages/p2`
  - ...

then you should do

- `touch pnpm-workspace.yaml`
  -
    ```yaml
    # pnpm-workspace.yaml
    packages:
      - 'packages/*'
      - 'app/*'
    ```

to define where the packages (as well as the apps) are

## declare dependencies resolve

- edit `package.json`
  - 
    ```js
    // package.json
    {
      "dependencies": {
        "p1": "workspace:*",
        "p2": "workspace:*"
        // ...
      }
    }
    ```

to define where to resolve packages

<!-- how to use wildcard character to avoid tedious job? -->

## create app(s) [to use packages]

- `mkdir app app/a1 app/a2`

- `pnpm init`

## create package(s) [to be used by apps or other packages]

- `mkdir packages packages/p1 packages/p2`

- `pnpm init`

- `touch packages/p1/index.js`
  -
    ```js
    export default {
      name: "I'm p1!"
    }
    ```

## import depencencies in app

- `touch app/a1/index.js`
  -
    ```js
    import p1 from 'p1'
    console.log(p1) // { name: "I'm p1!"}
    ```

## go!

- `pnpm install` - creat a `pnpm-lock.yaml`
- `node app/a1/index.js`

## Next: create more packages

- `mkdir packages packages/ui-web/ComponentA packages/ui-web/ComponentB ...`

- `pnpm init`

- edit `packages/ui-web/ComponentA/package.json`
  -
    ```js
    {
      "name": "@the-org/ui-web-ComponentA",
      // ...
    }
    ```
- edit `/root/package.json`
  -
    ```js
    {
      "@the-org/ui-web-ComponentA": "workspace:*"
      // ...
    }
    ```

- `touch packages/ui-web/ComponentA`
  -
    ```js
    export default {
      name: "I'm @the-org/ui-web-ComponentA!"
    }
    ```

