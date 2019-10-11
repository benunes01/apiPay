<h1>Como fazer uma API em Node</h1>
<h3>Passo a passo:</h3>

<p>A ideia aqui é você já ter uma noção, já que não será explicado todos os códigos escritos.</p>

<h2>Pré requisitos</h2>

<ul>
    <li>Node.js</li>
    <li>NPM ou Yarn</li>
    <li>VSCode*</li>
</ul>
<br>
<br>
<p>Irei utilizar o <b>Yarn</b> como gerenciador de dependências, fiquem livres para utilizar o NPM se assim preferir. Já como editor de código irei utilizar o <b>VSCode</b> um editor de código que me atrai bastante, porém, você é livre para utilizar qualquer
    outro editor a sua preferência.</p>

<h2>Passos</h2>

```Crie um Diretório e acesse ele pelo VSCode```
<br>
<h3>No terminal, dentro da pasta, execute:</h3>

```yarn init -y```
<br>
<li><b>init:</b> Essa instrução instrui o `yarn` a criar um arquivo `package.json`, responsável por guardar algumas definições iniciais do projeto e a lista de dependências</li>
<br>
<li><b>-y:</b> Ativa confirmação silenciosa, ou seja, preencher todas as perguntas com a resposta padrão, deste modo não seremos questionados quanto as escolhas durante o processo de criação, você é livre para remover o `-y` se assim preferir.</li>
<br>
<h3>Agora iremos instalar nossa primeira dependência, que ficará salva no package.json:</h3>

```yarn add express```
<br>
<li><b>Express:</b> Micro-framework simples e flexível</li>
<br>
<h4>Agora vamos criar a pasta 'src' na raiz do projeto. Onde ficará os códigos da nossa aplicação.</h4>
<h4>Iniciailmente, dentro da pasta 'src' teremos os arquivos: 'server.js' , 'app.js' e 'routes.js'.</h4>
<br>

<h4>Antes de continuar, devemos instalar mais duas dependências, a Nodemon e a sucrase:</h4>

```yarn nodemon sucrase -D```
<br>
<p>Repare que usamos o <b>-D</b> , é para ele colocar no 'package.json' como uma dependência de desenvolvimento.</p>
<br>
<li><b>nodemon: </b>Basicamente ele é um file watcher que roda internamente o próprio comando node, sempre que atualizarmos o código, não precisamos reiniciar o servidor, o nodemon faz isso automaticamente.</li>
<br>
<li><b>sucrase: </b>Ele é uma alternativa mais rápida ao babel. É um transpilador que nos possibilita a usar os novos padrões do javaScript, como ES6.</li>
<br>
<h4>Vamos configurar o projeto para que possamos usar o sucrase e nodemon de forma correta:</h4>
<br>
<h5>No arquivo <b>package.json</b> iremos adicionar em 'scripts' o seguinte código: "dev": "nodemon src/server.js"</h5>
<h4>O arquivo ficará assim:</h4>

```
./package.json

{
    "name": "api",
    "version": "1.0.0",
    "description": "api",
    "main": "index.js",
    "scripts": {
        "test": "echo \"Error: no test specified\" && exit 1",
        "dev": "nodemon src/server.js"
    },
    "author": "Bernardo",
    "license": "ISC",
    "dependencies": {
        "express": "^4.17.1",
    },
    "devDependencies": {
        "nodemon": "^1.19.3",
        "sucrase": "^3.10.1"
    }
}
```
<br>

<h4>Agora vamos criar o arquivo <b>nodemon.json</b> na raiz do projeto.</h4>
<h5>Dentro dele vamos colocar apenas: </h5>

```
{
    "execMap": {
        "js": "sucrase-node"
    }

}
```
<br>

<h4>Configurado, agora vamos criar a base da nossa aplicação, codificando os arquivos criados na pasta 'src'. <br>
    <br>
    Os arquivos devem ficar assim: 
</h4>

<h5>app.js</h5>

```
import express from 'express';
import routes from './routes';

class App {
  constructor() {
    this.server = express();

    this.middlewares();
    this.routes();
  }

  middlewares() {
    this.server.use(express.json());
  }

  routes() {
    this.server.use(routes);
  }
}

export default new App().server;
```
<br>

<h5>routes.js</h5>

```
import { Router } from 'express';

const routes = new Router();

routes.get('/', (req, res) => res.json({ message: 'Hello' }));

export default routes;
```
<br>

<h5>server.js</h5>

```
import app from './app';

app.listen(3000);

```

<h4>Agora se você for no terminal e colocar o comando: 'npm run dev' , irá iniciar o servidor normalmente. <br>
    <br>
    Indo no navegador e colocando  'localhost:3000', deverá aparecer em json {'message: 'hello'} .
</h4>
<br>
<h3>Com ele rodando perfeitamente, vamos adicionar mais algumas dependências que vai nos ajudar pelo resto da criação.</h3>

```yarn add eslint prettier eslint-config-prettier eslint-plugin-prettier babel-eslint```

<p>Obs: lembre-se de que além da instalação via NPM ou Yarn, é necessário acessar a "marketplace" do seu editor de código, no caso do VSCode, WebStorm, Sublame Text e outros, e instalar o plugin do ESLint e do Prettier para o editor de código ou IDE que
    está sendo utilizada. Consulte as instruções do seu editor/IDE para verificar como instalar plugins.</p>

<br>

<ul>
    <li>eslint: utilizado para análise de código estático e identificação de padrões problemáticos encontrados no código JavaScript.</li>
    <li> babel-eslint: aumenta a compatibilidade entre o ES6 (ECMAScript 6 — que é uma especificação da linguagem JavaScript) e o Eslint. Lembrando que o sucrase é bom apenas em ambiente de desenvolvimento.</li>
    <li>prettier: formata o código de modo a manter um padrão em todo o projeto, os plugins `eslint-config-prettier` e `eslint-plugin-prettier` cuidam de fazer a integração entre o ESLint e o Prettier, de modo a promover correções automáticas no código sempre
        que o ESLint apontar uma quebra de padrão/erro, obviamente você pode incluir regras personalizadas ou ignorar as predefinidas que não atenderem ao seu interesse.</li>
</ul>

<h5>Feito isso, vamos configurar o ESLint</h5>

```yarn eslint --init```

<br>

<h5>Abaixo são as opções de configuração, ai estão as respostas que eu considero para o questionário, você pode selecionar utilizando as setas para cima ou para baixo e pressionando enter.</h5>

<h4>Opção 1: define como o ESLint irá funcionar, verificando a sintaxe, rastreando problemas e forçando a aderência ao estilo.</h4>

```To check syntax, find problems, and enforce code style```

<h4>Define como será feito o import/export de módulos.</h4>

```JavaScript modules (import/export)```

<h4>Qual framwork estamos utilizando.</h4>

```None of these```

<h4>Define que o código irá rodar sobre o Node, ou seja, no back-end.</h4>
<br>
<p>Desmarca o 'Browser com a tecla 'ESPAÇO'</p>

```Node```

<h4>Define que utilizaremos um guia de estilos popular.</h4>

```Use a popular style guide```

<h4>define o Airbnb como style guide padrão do projeto.</h4>

```Airbnb```

<h4>Especifica que o arquivo de configurações do ESLint seguirá o formado JSON.</h4>

```JSON```

<br>

<h5>Escreva Y e aperte Enter</h5>

<br>

<h5>Caso esteja utilizando YARN, exclua o arquivo `package-lock.json` e execute a instrução abaixo, do contrário ignore somente essa instrução:</h5>

```yarn```

<br>

<h4>Edite o arquivo '.eslintrc.json' , ficando assim:</h4>

```
{
    "env": {
        "es6": true,
        "node": true
    },
    "extends": [
        "airbnb-base",
        "prettier"
    ],
    "globals": {
        "Atomics": "readonly",
        "SharedArrayBuffer": "readonly"
    },
    "parser": "babel-eslint",
    "parserOptions": {
        "ecmaVersion": 2018,
        "sourceType": "module"
    },
    "plugins": [
        "prettier"
      ],
    "rules": {
        "prettier/prettier": "error",
        "class-methods-use-this": "off",
        "no-param-reassign": "off",
        "camelcase": "off",
        "no-unused-vars": ["error", { "argsIgnorePattern": "next" }]
    }
}
```

<h4>Crie o arquivo '.prettierrc e adicione este conteúdo nele:</h4>

```
{
    "singleQuote": true,
    "trailingComma": "es5"
  }
```
<br>

<h4>Agora para organizar ainda mais, vamos criar mais alguns arquivos e pastas.</h4>
<br>
<ul>
    <li>Criar a pasta <b>config</b> dentro da pasta <b>src</b></li>
    <li>Criar o arquivo <b>database.js</b> dentro da pasta <b>config</b></li>
    <li>Criar a pasta <b>database</b> dentro da pasta <b>src</b></li>
    <li>Criar uma pasta <b>migrations</b> dentro da pasta <b>database</b></li>
    <li>Criar a pasta <b>app</b> dentro da pasta <b>src</b></li>
    <li>Criar a pasta <b>controllers</b> e a pasta <b>models</b> dentro da pasta <b>app</b></li>
</ul>

<br>

<h4>Agora vamos instalar o sequelize, que vai nos ajudar na criação do banco de dados.</h4>

```yarn add sequelize```

<br>

<h5>E esse:</h5>

<h5>Interface de linha de comando</h5>

```yarn add sequelize-cli -D```

<br>

<h4>Depois de instalado, vamos criar um arquivo na raix do projeto chamado <b>.sequelizerc</b>, deixando na sintaxe de JavaScript.</h4>

<br>

<h4>O arquivo vai ficar assim:</h4>

```
const { resolve } = require('path');

module.exports = {
    config: resolve(_dirname, 'src', 'config', 'database'),
    'models-path': resolve(_dirname, 'src', 'app', 'models'),
    'migrations-path': resolve(_dirname, 'src', 'database', 'migrations'),
    'seeders-path': resolve(_dirname, 'src', 'database', 'seeds'),
}
```

<h4>Feito isso, vamos no <b>database.js</b> dentro da pasta <b>config</b> e exportar um arquivo de configuração.</h4>

<br>

<h5>Vamos usar o Postgree para ser nosso banco de dados</h5>

```yarn add pg pg-hstore```

```
module.exports = {
    dialect: 'postgres',
    host: 'localhost',
    username: 'postgres',
    password: '123',
    database: 'becaptain',
    define: {
      timestamps: true,
      underscored: true,
      underscoredAll: true,
    },
  };
  ```
  
  <br>

<h4>Vamos fazer nossa primeira <b>Migration</b></h4>
<br>
<h5>Para facilitar vamos usar esse comando no terminal:</h5>

```yarn sequelize migration:create --name-create-users ```
<br>

<h5>Com isso vai ter criado o arquivo dentro da pasta <b>Migrations</b></h5>

<h5>Você pode tirar os exemplos e deixar apenas o return dentro do <b>Up</b> e do <b>Down</b></h5>

<h5>Vamos definir os campos na nossa tabela, o arquivo deve ficar assim:</h5>

```
// ./config/database/migrations/"arquivo criado"

up: (queryInterface, Sequelize) => {
    return queryInterface.createTable('users', {
        id: {
            type: Sequelize.INTEGER,
            allowNull: false,
            autoincrement: true,
            primaryKey: true,
    },
    name: {
        type: Sequelize.STRING,
        allowNull: false,
    },
    email: {
        type: Sequelize.STRING,
        allowNull: false,
        unique: true,
    },
    password_hash: {
        type: Sequelize.STRING,
        allowNull: false,
    },
    provider: {
        type: Sequelize.BOOLEAN,
        defaultValue: false,
        allowNull: false,
    },
    created_at:{
        type: Sequelize.DATE,
        allowNull: false,
    },
    update_at: {
        type: Sequelize.DATE,
        allowNull: false,
    }
    });
},

down: queryInterface => {
    return queryInterface.dropTable('users');
},
};
```
<h5>O <b>provide</b> é quando sua aplicação tem dois tipos de usuario, por exemplo: O cliente(false) e o Provedor(true).</h5>

<br>

<h4>Agora execute no terminal e o sequelize vai criar a tabela no banco de dados. </h4>

```yarn  sequelize dbmigrate```

<br>

<h5>Você pode usar o <b>PostBird</b> para verificar</h5>

<br>

<h4>Caso você ve que cometeu algum erro e ainda não enviou para os outros desenvolvedores, você pode usar o comando para desfazer:</h4>

```yarn sequelize db:migrate:undo```

<br>

<h4>Agora vamos criar o <b>model do usuario</b>, que vai ser usado para manipular os usuarios.</h4>
<br>
<h5>Crie o arquivo <b>User.js</b> dentro da pasta <b>models</b></h5>

<br>
<h5>O arquivo deve ficar assim:</h5>

```
import Sequelize, { Model } from 'sequelize'; 

    class User extends Model {
        static init(sequelize) {
            super.init({
                name: Sequelize.STRING,
                email: Sequelize.STRING,
                password_hash: Sequelize.STRING,
                provider: Sequelize.BOOLEAN,
            },
            {
                sequelize,
            }
            );
        }
    }

    export default User;

```

<br>

<h5>Agora com o model criado, precisamos carregar para ele ser usado na nossa aplicação</h5>

<br>

<h4>Dentro da pasta <b>database</b>, vamos criar o arquivo <b>index.js</b>, ele ficará assim: </h4>

```
import Sequelize from 'sequelize';

import User from '../app/models/User';

import databaseConfig from '../config/database';

const models = [User];

class database {
    constructor() {
        this.init();
    }

    init() {
        this.connection = new Sequelize(databaseConfig);

        models.map(model => model.init(this.connection));
    }
}

export default new Database();

```

<br>

<h4>Também devemos importar ele no arquivo <b>app.js</b> e no <b>User.js</b></h4>

```
//app.js

import express from 'express';
import routes from './routes';

import './database';

class App {
  constructor() {
    this.server = express();

    this.middlewares();
    this.routes();
  }

  middlewares() {
    this.server.use(express.json());
  }

  routes() {
    this.server.use(routes);
  }
}

export default new App().server;

```

<br>

<h5>Depois vamos tirar nossa logica do routes e colocar no controller, mas por enquanto vai ficar ali.</h5>

```
// route.js

import { Router } from 'express';

import User from './app/models/User';

const routes = new Router();

routes.get('/', (req, res) => res.json({ message: 'Hello' }));

export default routes;

```
