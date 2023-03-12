# stylelint-sass-parse-error

This repository contains the code causing `Error: The node source must be present` stylelint error.

Test [code](./src/index.sass):

```sass
@media screen and (max-width: 744px)
  .container
    flex: 1 1 100%
```

## Description

The project uses `postcss-sass` custom syntax in Stylelint configuration, on top of `stylelint-config-standard`, for `*.sass` files.

There are two Stylelint configs: [`.stylelintrc_default.json`](./.stylelintrc_default.json), which throws, and [`.stylelintrc_rules.json`](./.stylelintrc_rules.json) with some rules disabled to avoid throwing.

When we run `npm run lint:default`, the default configuration is used. This throws an error:

```PowerShell
npm run lint:default

> stylelint-sass-parse-error@1.0.0 lint:default
> stylelint "./src/**" --config .stylelintrc_default.json

Error: The node source must be present
    at Object.getContext (C:\Users\dmytr\Projects\stylelint-sass-parse-error\node_modules\stylelint\lib\utils\nodeContextLookup.js:23:28)
    at C:\Users\dmytr\Projects\stylelint-sass-parse-error\node_modules\stylelint\lib\rules\no-descending-specificity\index.js:72:52
    at C:\Users\dmytr\Projects\stylelint-sass-parse-error\node_modules\postcss\lib\container.js:96:18
    at C:\Users\dmytr\Projects\stylelint-sass-parse-error\node_modules\postcss\lib\container.js:55:18
    at Root.each (C:\Users\dmytr\Projects\stylelint-sass-parse-error\node_modules\postcss\lib\container.js:41:16)
    at Root.walk (C:\Users\dmytr\Projects\stylelint-sass-parse-error\node_modules\postcss\lib\container.js:52:17)
    at Root.walkRules (C:\Users\dmytr\Projects\stylelint-sass-parse-error\node_modules\postcss\lib\container.js:94:19)
    at C:\Users\dmytr\Projects\stylelint-sass-parse-error\node_modules\stylelint\lib\rules\no-descending-specificity\index.js:60:8
    at C:\Users\dmytr\Projects\stylelint-sass-parse-error\node_modules\stylelint\lib\lintPostcssResult.js:114:8
    at Array.map (<anonymous>)
```

As a result of disabling problematic rules `parseError` occurs, which is listed as linter error:

```PowerShell
npm run lint:rules

> stylelint-sass-parse-error@1.0.0 lint:rules
> stylelint "./src/**" --config .stylelintrc_rules.json


src/index.sass
      ✖  Cannot parse selector (TypeError: Cannot read properties of undefined (reading 'start'))  parseError

1 problem (1 error, 0 warnings)
```
