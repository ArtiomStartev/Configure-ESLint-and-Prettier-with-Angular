# Configure ESLint and Prettier with Angular 🚀

### **Install and configure ESLint**:

> [!NOTE]
> By statically analyzing our code, ESLint can find problems and also suggest fixes for them. And it can do better than that, it can fix our code automatically.</br>
 - Open the terminal and install ESLint schematics using this command:</br>
   ```
   ng add @angular-eslint/schematics
   ```
   
- We can also run this command in the terminal to fix all the fixable bugs in the project:</br>
  ```
  ng lint --fix
  ```
  
### **Install and configure Prettier**:

> [!NOTE]
> Even if we have ESLint watching our code for bugs, we also need a tool to better style and format it. That’s where Prettier comes into play. Prettier is an opinionated code formatter that helps us beautify code in a standardized way every time we save the code.</br>
 - Open the terminal and install Prettier using this command:</br>
   ```
   npm install prettier --save-dev
   ```

 - OR if you’re using yarn :
   ```
   yarn add prettier -D
   ```

> [!IMPORTANT]
> Then we need to add **.prettierrc.json** and **.prettierignore** files in our root project directory.</br>
  ```
  touch .prettierrc.json
  ```
  ```
  touch .prettierignore
  ```
</br>

 - Inside **.prettierrc.json** we can change the default settings by overriding them.
  ```
{
    "tabWidth": 2,
    "useTabs": false,
    "singleQuote": true,
    "semi": true,
    "bracketSpacing": true,
    "trailingComma": "none",
    "bracketSameLine": true,
    "printWidth": 120
}
```
</br>

- Inside the **.prettierignore** file I put the following:
```
  build/*
  bin/*
  public/*
  certs/*
  coverage/*
  node_modules/
  .idea/*
  .husky/*
```
</br>

- We can then run this command inside our project to format it.

  ```
  npx prettier --write .
  ```


### **Configure Prettier to be used as an ESLint plugin:**

> [!NOTE]
> For ESLint and Prettier to play well together, we need to run Prettier as an ESLint plugin. This way we can just call `ng lint — fix` and ESLint will fix bugs but also format the code.

- Open the terminal and type:

  ```
  npm install prettier-eslint eslint-config-prettier eslint-plugin-prettier --save-dev
  ```

- OR if you’re using yarn :

  ```
  yarn add prettier-eslint eslint-config-prettier eslint-plugin-prettier -D
  ```
</br>

- Now we need to edit the **.eslintrc.json** file to include the Prettier plugin:
```
{
  "root": true,
  "ignorePatterns": ["projects/**/*"],
  "overrides": [
    {
      "files": ["*.ts"],
      "parserOptions": {
        "project": ["tsconfig.json"],
        "createDefaultProgram": true
      },
      "extends": [
        "plugin:@angular-eslint/recommended",
        "plugin:@angular-eslint/template/process-inline-templates",
        "plugin:prettier/recommended"
      ],
      "rules": {
        "@angular-eslint/component-class-suffix": [
          "error",
          {
            "suffixes": ["Page", "Component"]
          }
        ],
        "@angular-eslint/component-selector": [
          "error",
          {
            "type": "element",
            "prefix": "app",
            "style": "kebab-case"
          }
        ],
        "@angular-eslint/directive-selector": [
          "error",
          {
            "type": "attribute",
            "prefix": "app",
            "style": "camelCase"
          }
        ],
        "@typescript-eslint/member-ordering": 0,
        "@typescript-eslint/naming-convention": 0
      }
    },
    {
      "files": ["*.html"],
      "extends": ["plugin:@angular-eslint/template/recommended"],
      "rules": {}
    },
    {
      "files": ["*.html"],
      "excludedFiles": ["*inline-template-*.component.html"],
      "extends": ["plugin:prettier/recommended"],
      "rules": {
        "prettier/prettier": ["error", { "parser": "angular" }]
      }
    }
  ]
}

```
</br>

> [!NOTE]
> After we edit a file, we want to format it and then save it. First, make sure you have the **ESLint** and **Prettier** plugins installed. **IntelliJ IDEA** has support out-of-the-box for both.

<img width="985" alt="Screenshot 2023-10-28 at 11 50 21" src="https://github.com/ArtiomStartev/Configure-ESLint-and-Prettier-with-Angular/assets/96334648/7ac7e5ec-4e8c-4e54-9934-128e7ddfc5a9"></br>

> [!NOTE]
> And add the following property to the **package.json** file inside the **"scripts"** object:
```
"lint": "ng lint --fix"
```
