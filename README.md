# Static check with next 11 (Prettier, ESLint)

## Visual Studio Code
First things first, configure your VSCode and add needed plugins.
- Install ESLint plugin for VSCode. 
- 🚫 Prettier plugin for VSCode is not needed.
- Add this configuration on your VSCode Settings:
  ```json
  "editor.formatOnSave": false,
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  },
  ```

## Start your project
```shell
# js project
$ yarn create next-app staticcheck_jsproject

# ts project
$ yarn create next-app staticcheck_tsproject --ts
```

## Know what NEXT delivers

  Next is shiped with some ESLint configurations out of the box. The project will be created with this ESLint rules
  - eslint-plugin-react
    - plugin:react/recommended
  - eslint-plugin-react-hooks
    - plugin:react-hooks/recommended
  - eslint-plugin-next
    - plugin:@next/next/recommended
  - eslint-plugin-jsx-a11y (not present in documentation, but searching in node_modules seems to be present)
    - alt-text: this seems to be the only present rule, [see more about this rule](https://github.com/jsx-eslint/eslint-plugin-jsx-a11y/blob/master/docs/rules/alt-text.md)

## Improve the basic
The basic configuration can be found at the root of the project, in `.eslintrc` file.

```json
{
  "extends": ["next", "next/core-web-vitals"]
}
```

1. Enable `eslint:recommended`. [See all rules ](https://eslint.org/docs/rules/)

    ```json
    {
      "extends": [
        "eslint:recommended",
        "next", 
        "next/core-web-vitals"
      ]
    }
    ```
2. Maybe improve accessibility rules? [See all rules](https://github.com/jsx-eslint/eslint-plugin-jsx-a11y#rule-strictness-in-different-modes)
    ```json
    {
      "extends": [
        "eslint:recommended",
        "plugin:jsx-a11y/recommended",
        "next", 
        "next/core-web-vitals"
      ]
    }
    ```
3. Inform your environment (I need to investigate in node_modules if `env` is needed)
    ```json
    {
      "env": {
        "browser": true,
        "es2021": true,
        "node": true
      },
      "extends": [
        "eslint:recommended",
        "next", 
        "next/core-web-vitals"
      ]
    }
    ```

## Code formatter time. Prettier, fix this.
Now your project is very colorful, it looks like carnaval in Brazil, many red and blue squiggles (fix it soon, please 🙏🏽), but we need to take care of the code format.

1. Install packages for prettier
```shell
$ yarn add -D prettier eslint-plugin-prettier eslint-config-prettier
```

2. Create an `.prettierrc` file at the root of your project and define some rules. [See more options](https://prettier.io/docs/en/options.html)
```json
{
	"trailingComma": "none",
	"semi": false,
	"singleQuote": true
}
```

3. Let ESLint know who the chef is in the format.
```json
{
  "env": {
    "browser": true,
    "es2021": true,
    "node": true
  },
  "extends": [
    "eslint:recommended",
    "next", 
    "next/core-web-vitals",
    "plugin:prettier/recommended" // always at the end
  ]
}
```
Now your code will be formated when you save any file.

<!-- OLD, based only in docs -->

<!--  

Next is shiped with some ESLint configurations out of the box. Some considerations about this:
- extends
  - `next`: this extends recommended rule sets from various ESLint plugins like:
    - eslint-plugin-react
    - eslint-plugin-react-hooks
    - eslint-plugin-next
  - `plugin:react/recommended`: This can be removed, next extend this configuration.
  - `next/core-web-vitals`: This update `eslint-plugin-next` transforming warnnings in errors. If you are happy with warnnings don't use this.
- rules
  - The rules below can/ should be removed, this rules are present in `eslint-plugin-next`
    - react/prop-types": "off
    - react/react-in-jsx-scope": "off

## Basic configuration (not shiped with next11)
```shell
$ yarn add -D @typescript-eslint/parser @typescript-eslint/eslint-plugin prettier eslint-plugin-prettier eslint-config-prettier
```
Basic `.eslintrc`
```json
{
  "env": {
    "browser": true,
    "es2021": true,
    "node": true
  },
  "extends": [
    "eslint:recommended",
    "plugin:@typescript-eslint/recommended",
    "next", 
    "next/core-web-vitals",
    "plugin:prettier/recommended"
  ],
  "parser": "@typescript-eslint/parser",
  "parserOptions": {
    "ecmaFeatures": {
        "jsx": true
    },
    "ecmaVersion": 12,
    "sourceType": "module"
  },
  "plugins": ["@typescript-eslint"],
  "rules": {
    "react-hooks/rules-of-hooks": "error",
    "react-hooks/exhaustive-deps": "warn",
    "@typescript-eslint/explicit-module-boundary-types": "off"
  }
}

```

Basic `.prettierrc`

```json
{
  "trailingComma": "none",
  "semi": false,
  "singleQuote": true
}
```

-->