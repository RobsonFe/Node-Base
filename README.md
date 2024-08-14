# Criando-API-Node-TypeScript

- Nesse README mostro como criar uma API Node com TypeScript.
- Seguindo esse passo a passo, voce será capaz de utilizar a configuração que geralmente utilizo nos meus projetos em Node.
---
## Iniciar a aplicação Node.js com Typescript
```node
npm init -y

# ou

yarn init -y
```
- Fazer a instalação do Typescript na pasta do projeto, como uma dependência de desenvolvimento. Como o código final é convertido para javascript antes de ser disponibilizado online, só precisaremos do Typescript em ambiente de desenvolvimento.

```node
npm install typescript ts-node-dev @types/node tsconfig-paths -D

# ou

yarn add typescript ts-node-dev @types/node tsconfig-paths -D
```
- Foi adicionado o pacote `tsconfig-paths` para também ser instalado. Esse pacote servirá para criação de atalhos para os paths de arquivos ao usar o `import`.
---
- Criar o arquivo "`tsconfig.json`" que conterá as configurações do Typescript, com o comando:

```node
npx tsc --init --rootDir src --outDir build --esModuleInterop --resolveJsonModule --lib es6 --module commonjs --allowJs true --noImplicitAny true
```
---
Em resumo, os parâmetros passados são:

`rootDir`: É aqui que o TypeScript procura nosso código.

`outDir`: Onde o TypeScript coloca nosso código compilado.

`esModuleInterop`: Se estiver usando commonjs como sistema de módulo (recomendado para aplicativos Node), então esse parâmetro deve ser definido como true.

`resolveJsonModule`: Se usarmos JSON neste projeto, esta opção permite que o TypeScript o use.

`lib`: Esta opção adiciona tipos de ambiente ao nosso projeto, permitindo-nos contar com recursos de diferentes versões do Ecmascript, bibliotecas de teste e até mesmo a API DOM do navegador. Usaremos recursos es6 da linguagem.

`module`: commonjs é o sistema de módulo Node padrão.

`allowJs`: Se você estiver convertendo um projeto JavaScript antigo em TypeScript, esta opção permitirá que você inclua arquivos .js no projeto.

`noImplicitAny`: Em arquivos TypeScript, não permita que um tipo seja especificado inexplicitamente. Cada tipo precisa ter um tipo específico ou ser declarado explicitamente any.

---
Nosso arquivo `tsconfig.json` deve estar assim:

```node
{
  "compilerOptions": {
    /* Visit https://aka.ms/tsconfig.json to read more about this file */

    /* Basic Options */
    // "incremental": true,                   /* Enable incremental compilation */
    "target": "es5",                          /* Specify ECMAScript target version: 'ES3' (default), 'ES5', 'ES2015', 'ES2016', 'ES2017', 'ES2018', 'ES2019', 'ES2020', or 'ESNEXT'. */
    "module": "commonjs",                     /* Specify module code generation: 'none', 'commonjs', 'amd', 'system', 'umd', 'es2015', 'es2020', or 'ESNext'. */
    // "lib": ["es6"],                           /* Specify library files to be included in the compilation. */
    "allowJs": true,                          /* Allow javascript files to be compiled. */
    // "checkJs": true,                       /* Report errors in .js files. */
    // "jsx": "preserve",                     /* Specify JSX code generation: 'preserve', 'react-native', or 'react'. */
    // "declaration": true,                   /* Generates corresponding '.d.ts' file. */
    // "declarationMap": true,                /* Generates a sourcemap for each corresponding '.d.ts' file. */
    // "sourceMap": true,                     /* Generates corresponding '.map' file. */
    // "outFile": "./",                       /* Concatenate and emit output to single file. */
    "outDir": "./build",                        /* Redirect output structure to the directory. */
    "rootDir": "./src",                         /* Specify the root directory of input files. Use to control the output directory structure with --outDir. */
    // "composite": true,                     /* Enable project compilation */
    // "tsBuildInfoFile": "./",               /* Specify file to store incremental compilation information */
    // "removeComments": true,                /* Do not emit comments to output. */
    // "noEmit": true,                        /* Do not emit outputs. */
    // "importHelpers": true,                 /* Import emit helpers from 'tslib'. */
    // "downlevelIteration": true,            /* Provide full support for iterables in 'for-of', spread, and destructuring when targeting 'ES5' or 'ES3'. */
    // "isolatedModules": true,               /* Transpile each file as a separate module (similar to 'ts.transpileModule'). */

    /* Strict Type-Checking Options */
    "strict": true,                           /* Enable all strict type-checking options. */
    "noImplicitAny": true,                    /* Raise error on expressions and declarations with an implied 'any' type. */
    // "strictNullChecks": true,              /* Enable strict null checks. */
    // "strictFunctionTypes": true,           /* Enable strict checking of function types. */
    // "strictBindCallApply": true,           /* Enable strict 'bind', 'call', and 'apply' methods on functions. */
    "strictPropertyInitialization": false,  /* Enable strict checking of property initialization in classes. */
    // "noImplicitThis": true,                /* Raise error on 'this' expressions with an implied 'any' type. */
    // "alwaysStrict": true,                  /* Parse in strict mode and emit "use strict" for each source file. */

    /* Additional Checks */
    // "noUnusedLocals": true,                /* Report errors on unused locals. */
    // "noUnusedParameters": true,            /* Report errors on unused parameters. */
    // "noImplicitReturns": true,             /* Report error when not all code paths in function return a value. */
    // "noFallthroughCasesInSwitch": true,    /* Report errors for fallthrough cases in switch statement. */
    // "noUncheckedIndexedAccess": true,      /* Include 'undefined' in index signature results */

    /* Module Resolution Options */
    "moduleResolution": "node",            /* Specify module resolution strategy: 'node' (Node.js) or 'classic' (TypeScript pre-1.6). */
    "baseUrl": ".",                       /* Base directory to resolve non-absolute module names. */
    // "paths": {},                           /* A series of entries which re-map imports to lookup locations relative to the 'baseUrl'. */
    // "rootDirs": [],                        /* List of root folders whose combined content represents the structure of the project at runtime. */
    // "typeRoots": [],                       /* List of folders to include type definitions from. */
    // "types": [],                           /* Type declaration files to be included in compilation. */
    // "allowSyntheticDefaultImports": true,  /* Allow default imports from modules with no default export. This does not affect code emit, just typechecking. */
    "esModuleInterop": true,                  /* Enables emit interoperability between CommonJS and ES Modules via creation of namespace objects for all imports. Implies 'allowSyntheticDefaultImports'. */
    // "preserveSymlinks": true,              /* Do not resolve the real path of symlinks. */
    // "allowUmdGlobalAccess": true,          /* Allow accessing UMD globals from modules. */

    /* Source Map Options */
    // "sourceRoot": "",                      /* Specify the location where debugger should locate TypeScript files instead of source locations. */
    // "mapRoot": "",                         /* Specify the location where debugger should locate map files instead of generated locations. */
    // "inlineSourceMap": true,               /* Emit a single file with source maps instead of having a separate file. */
    // "inlineSources": true,                 /* Emit the source alongside the sourcemaps within a single file; requires '--inlineSourceMap' or '--sourceMap' to be set. */

    /* Experimental Options */
    "experimentalDecorators": true,        /* Enables experimental support for ES7 decorators. */
    "emitDecoratorMetadata": true,         /* Enables experimental support for emitting type metadata for decorators. */

    /* Advanced Options */
    "resolveJsonModule": true,                /* Include modules imported with '.json' extension */
    // "skipLibCheck": true,                     /* Skip type checking of declaration files. */
    "forceConsistentCasingInFileNames": true, /* Disallow inconsistently-cased references to the same file. */
  },
  "exclude": [
    "node_modules",
    "build"
  ],
  "include": [
    "src/**/*"
  ]
}
```

## Arquivo .gitignore

```
.idea/
.vscode/
node_modules/
build/
temp/
.env
coverage
ormconfig.json
dist

uploads/*
!uploads/.gitkeep
````

Criar a pasta uploads com o arquivo `.gitkeep` dentro para que os arquivos carregados nessa pasta não sejam incluídos no controle de versão do Git.

- Criar a pasta `src` e o primeiro arquivo:

```bash
mkdir src

touch src/server.ts
```
- Código inicial do arquivo:

```node
console.log('Hello Dev!')
```

## Compilando o Typescript

- Para compilar nosso código, precisaremos executar o comando `tsc`, que irá ler o arquivo `tsconfig.json` no diretório atual e aplicará a configuração ao compilador TypeScript para gerar o código JavaScript compilado.

```node
npx tsc
```

O código compilado foi gerado na pasta `build`.

Executar o servidor em desenvolvimento

Usaremos a biblioteca `ts-node-dev` para execução da aplicação em desenvolvimento.

Incluir o script para rodar o `ts-node-dev` no arquivo `package.json`.

```node
"scripts": {
  "dev": "ts-node-dev --inspect --transpile-only --ignore-watch node_modules src/server.ts"
}
```

Executar o servidor:

```node
npm run dev

# ou

yarn dev
```

--- 

# EditorConfig
## O Editor Config é uma ferramenta que auxilia na padronização da configuração para vários desenvolvedores trabalhando em um mesmo projeto, mas em diferentes editores de código ou IDE's.

- O Editor Config é uma ferramenta que auxilia na padronização da configuração para vários desenvolvedores trabalhando em um mesmo projeto, mas em diferentes editores de código ou IDE's.
```vscode
Instalar no VSCode a extensão EditorConfig for VS Code.
```

Depois de instalada, ao clicar com o botão direito sobre o explorador de arquivos do projeto vamos selecionar a opção `Generate .editorconfig.`

E a execução dessa opção deve gerar um arquivo `.editorconfig` com o seguinte conteúdo:

```vscode
# EditorConfig is awesome: https://EditorConfig.org

# top-most EditorConfig file
root = true

[*]
indent_style = space
indent_size = 2
charset = utf-8
trim_trailing_whitespace = false
insert_final_newline = false
```
Nesse arquivo podemos ver algumas opções como o tipo de indentação, o tamanho da indentação, qual o charset que está sendo utilizado e algumas outras configurações.

O que vamos modificar nesse arquivo são apenas as opções, `trim_trailing_whitespace` e `insert_final_newline`, que devem ser modificadas de `false` para `true` e pessoalmente gosto de utilizar o `indent_size = 4` .

Além de adicionar uma última opção, a `end_of_line = lf` , para garantir que as quebras de linha sejam padronizadas, pois em linguagem de código, no Windows o final das linhas são representadas por `\r\n` , já no Linux é apenas com `\n` , e para evitar que isso gere algum tipo de problema ao mudar de Sistema Operacional, essa opção é adicionada.

O arquivo final vai ficar assim:

```vscode
# EditorConfig is awesome: https://EditorConfig.org

# top-most EditorConfig file
root = true

[*]
indent_style = space
indent_size = 4
end_of_line = crlf
charset = utf-8
trim_trailing_whitespace = false
insert_final_newline = true
end_of_line = lf
```

# ESLint

## ESLint é um linter JavaScript que permite que você aplique um conjunto de padrões de estilo, formatação e codificação para sua base de código. Ele examina seu código e avisa quando você não está seguindo o padrão que definiu.

---
## Instalação e Configuração do ESLint

- ESLint é um linter JavaScript que permite que você aplique um conjunto de padrões de estilo, formatação e codificação para sua base de código. Ele examina seu código e avisa quando você não está seguindo o padrão que definiu.

Instalação do ESLint no projeto:

```vscode
yarn add -D eslint @typescript-eslint/parser @typescript-eslint/eslint-plugin
```

- Na raiz do seu projeto crie um arquivo .eslintrc com uma configuração inicial do ESLint:

```json
{
  "root": true,
  "parser": "@typescript-eslint/parser",
  "plugins": [
    "@typescript-eslint"
  ],
  "extends": [
    "eslint:recommended",
    "plugin:@typescript-eslint/eslint-recommended",
    "plugin:@typescript-eslint/recommended"
  ]
}
```

Criar o arquivo `.eslintignore`:

```vscode
node_modules
dist
build
/*.js
```

Adicionar um script no arquivo `package.json` para executar o lint:

```json
{
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "dev": "ts-node-dev --inspect --transpile-only --ignore-watch node_modules src/server.ts",
    "lint": "eslint . --ext .ts"
  }
}

```

Esse comando faz basicamente com que o ESLint analise todos os arquivos dentro do projeto, indicando erros detectados de acordo com a configuração.

Execute o script e verifique que nenhum erro deve ser retornado.

```bash
yarn lint
```

## Adicionando regras
No arquivo `.eslintrc`, podemos adicionar o atributo rules ao objeto `json` para definição de regras.

Para cada regra podemos atribuir os seguintes valores: `"off"`, `"warn"` ou `"error"`.

```json
{
  "root": true,
  "parser": "@typescript-eslint/parser",
  "plugins": [
    "@typescript-eslint"
  ],
  "extends": [
    "eslint:recommended",
    "plugin:@typescript-eslint/eslint-recommended",
    "plugin:@typescript-eslint/recommended"
  ],
  "rules": { 
    "no-console": "warn"
  }
}
```

A regra no-console irá indicar se há algum `console.log()` perdido pelo código.

## Correção automática
O ESLint pode receber um parâmetro `--fix` para que tente corrigir automaticamente os problemas encontrados.

Vamos configurar outro script com a opção `--fix`.

```json
"scripts": {
  "test": "echo \"Error: no test specified\" &amp;&amp; exit 1",
  "dev": "ts-node-dev --inspect --transpile-only --ignore-watch node_modules src/server.ts",
  "lint": "eslint . --ext .ts",
  "lint-fix": "eslint . --ext .ts --fix"
}
```

# Prettier

## Prettier é um formatador de código opinativo e, em conjunto com o ESLint, forma uma parceria perfeita para nós, desenvolvedores.

--- 

## Instalação e Configuração do Prettier

Prettier é um formatador de código opinativo e, em conjunto com o ESLint, forma uma parceria perfeita para nós, desenvolvedores:

- ESLint define as convenções de código.
- Prettier realiza a formatação automática com base nas regras ESLint.

Instalação:

```vscode

yarn add prettier -D
```

Criar o arquivo .prettierrc com uma configuração básica do Prettier:

```json
{
  "semi": true,
  "trailingComma": "all",
  "singleQuote": true,
  "printWidth": 80,
  "arrowParens": "avoid"
}
```

Os parâmetros são:

`semi:` definido como `true`, significa que o Prettier adicionará ponto-e-vírgulas quando necessário.

`trailingComma:` definido como `all`, significa que o Prettier colocará vírgulas no final dos objetos.

`singleQuote:` definido como `true`, significa que o Prettier usará automaticamente aspas simples em vez de aspas duplas.

`printWidth:` definido como `80`, especifica que a impressora quebrará todas as linhas que excederem 80 caracteres.

É fundamental que extensão `Prettier – Code Formatter` esteja instalada no `VSCode`, pois permitirá a formatação automática do código ao salvar o arquivo.

Verifique se a sua configuração do `VS Code` possui os parâmetro:

```json
"editor.formatOnPaste": true,
"editor.formatOnType": true,
"formattingToggle.affects": ["formatOnSave"]
```
Essas configurações formatarão seu código quando você colar o novo código e quando você salvar o código de qualquer extensão de arquivo que o Prettier entende.

## Configurando o Prettier para trabalhar com ESLint

Com ESLint e Prettier já instalados, instale esses dois pacotes também:

```vscode
yarn add eslint-config-prettier@6.15.0 eslint-plugin-prettier@3.2.0 -D
```

`eslint-config-prettier`: Desativa todas as regras ESLint que têm o potencial de interferir com as regras do Prettier.

`eslint-plugin-prettier`: Transforma regras do Prettier em regras ESLint.

Ajustar o arquivo `.eslintrc`:

```vscode
{
  "root": true,
  "parser": "@typescript-eslint/parser",
  "plugins": [
    "@typescript-eslint",
    "prettier"
  ],
  "extends": [
    "eslint:recommended",
    "plugin:@typescript-eslint/eslint-recommended",
    "plugin:@typescript-eslint/recommended",
    "prettier/@typescript-eslint",
    "plugin:prettier/recommended"
  ],
  "rules": {
    "no-console": "warn",
    "prettier/prettier": "error"
  }
}
```
---
### Estrutura do Projeto

Estrutura de pastas:

`config` - configurações de bibliotecas externas, como por exemplo, autenticação, upload, email, etc.

`modules` - abrangem as áreas de conhecimento da aplicação, diretamente relacionados com as regras de negócios. A princípio criaremos os seguintes módulos na aplicação: customers, products, orders e users.

`shared` - módulos de uso geral compartilhados com mais de um módulo da aplicação, como por exemplo, o arquivo server.ts, o arquivo principal de rotas, conexão com banco de dados, etc.

`services` - estarão dentro de cada módulo da aplicação e serão responsáveis por todas as regras que a aplicação precisa atender, como por exemplo:

- A senha deve ser armazenada com criptografia;
- Não pode haver mais de um produto com o mesmo nome;
- Não pode haver um mesmo email sendo usado por mais de um usuário;
- E muitas outras...

Criando a estrutura de pastas:

```shell
mkdir -p src/config
````
```shell
mkdir -p src/modules
```
```shell
mkdir -p src/shared/http
```
```shell
mv src/server.ts src/shared/http/server.ts
```

Ajustar o arquivo `package.json`:

```json
{
  "scripts": {
    "dev": "ts-node-dev --inspect --transpile-only --ignore-watch node_modules src/shared/http/server.ts"
  }
}
```

### Configurando as importações

Podemos usar um recurso que facilitará o processo de importação de arquivos em nosso projeto.

Iniciamos configurando o objeto `paths` do `tsconfig.json`, que permite criar uma base para cada `path` a ser buscado no projeto, funcionando de forma similar a um atalho:

```json
"paths": {
  "@config/*": ["/src/config/*"],
  "@modules/*": ["/src/modules/*"],
  "@shared/*": ["/src/shared/*"]
}
```

Ficou faltando instalar a biblioteca que irá indicar ao nosso script do `ts-node-dev`, como interpretar os atalhos que configuramos iniciando com o caracter `@`.

O nome dessa biblioteca é `tsconfig-paths`, e para instalar execute o seguinte comando no terminal (na pasta do projeto):

```shell
yarn add -D tsconfig-paths
```

Depois de instalar o `tsconfig-paths`, ajustar o script `dev` no arquivo `package.json`, incluindo a opção `-r tsconfig-paths/register`. Deverá ficar assim:

```json
"dev": "ts-node-dev -r tsconfig-paths/register --inspect --transpile-only --ignore-watch node_modules src/shared/http/server.ts"
```

> Observação: o comando acima deve ser incluído como uma linha única do script `dev`.


Agora, para importar qualquer arquivo no projeto, inicie o caminho com um dos `paths` configurados, usando o `CTRL+SPACE` para usar o autocomplete.

---

Autor: [Robson Ferreira](https://github.com/RobsonFe) 
