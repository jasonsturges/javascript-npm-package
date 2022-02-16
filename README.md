# NPM Package Boilerplate

Scaffold JavaScript npm packages using this template to bootstrap your next library.

This boilerplate supports generating TypeScript declarations (`d.ts`) for compatibility with TypeScript projects by using JSDoc comments for types.

Project includes:
- [TypeScript](https://www.typescriptlang.org/)
- [Rollup](https://rollupjs.org/)
- [Microsoft API Extractor](https://api-extractor.com/)
- [TypeDoc](https://typedoc.org/)

_For a TypeScript version of this boilerplate, see: https://github.com/jasonsturges/npm-package-boilerplate_


## Getting Started

Begin via any of the following:

- Press the "*Use this template*" button

- Use [degit](https://github.com/Rich-Harris/degit) to execute:

    ```
    degit github:jasonsturges/npm-package-boilerplate
    ```

- Use [GitHub CLI](https://cli.github.com/) to execute:

    ```
    gh repo create <name> --template="https://github.com/jasonsturges/npm-package-boilerplate"
    ```

- Simply `git clone`, delete the existing .git folder, and then:

    ```
    git init
    git add -A
    git commit -m "Initial commit"
    ````

Remember to use `npm search <term>` to avoid naming conflicts in the NPM Registery for your new package name.


## Usage

The following tasks are available for `npm run`:

- `dev`: Run Rollup in watch mode to detect changes to files during development
- `build`: Run Rollup to build a production release distributable
- `build:types`: Run Microsoft API Extractor to rollup a types declaration (`d.ts`) file 
- `docs:jsdoc`: JSDoc generated documentation in the "*docs/*" folder
- `docs:typedoc`: TypeDoc for TSDoc generated documentation in the "*docs/*" folder
- `clean`: Remove all build artifacts


## Development

While test driven development (TDD) would be a good approach to develop your library, also consider creating an app for prototyping and local testing of your library.

**From your library project**, issue the `npm link` (or `yarn link`) command:

```
npm link
```

Start Rollup in watch mode:

```
npm run dev
```

**Create a test app project**, by doing the following:

To use your npm package library locally for development, create a new project in a separate folder:

```
mkdir test-app && cd test-app
npm init
```

Take the defaults from `npm init`

In the package.json of your test app, add the following two things:
- Set the `type` of your package to `module`
- Add a `start` script to execute your app

```json
"type": "module",
"scripts": {
  "start": "node index.js",
},
```

Link to your library using the `npm link <name>` (or `yarn link <name>`) command - be sure the `<name>` matches your library's package.json name.  For example:

```
npm link npm-package-boilerplate
```

Now, run your app via `npm start`.

As an example, if your library's "*index.ts*" file contained:

```ts
export const sayHi = () => {
  console.log("Hi");
};
```

...your test app would implement an import using your package name, such as:

```ts
import { sayHi } from "npm-package-boilerplate";

sayHi();
```


## Development Cleanup

Once development completes, `unlink` both your library and test app projects.

**From your test app project**, unlink the library using `npm unlink <name>` (or `yarn unlink <name>`) command:

```
npm unlink npm-package-boilerplate
```

**From your library project**, issue the `npm unlink` (or `yarn unlink`) command:

```
npm unlink
```


## Release Publishing

Once ready to submit your package to the NPM Registry, execute the following tasks via `npm` (or `yarn`):

- `npm run clean` &mdash; Assure a clean build
- `npm run build` &mdash; Build the JavaScript package
- `npm run build:types` &mdash; Build API Extractor (d.ts declarations) for TypeScript compatibility

Assure the proper npm login:

```
npm login
```

Submit your package to the registry:

```
npm publish --access public
```
