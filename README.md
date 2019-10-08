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
<li><b>sucrase: </b>Ele é uma alternativa mais rápida ao babel. É um trasnpilador que nos possibilita a usar os novos padrões do javaScript, como ES6.</li>
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

