# Static check with next 11 (Prettier, ESLint)
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