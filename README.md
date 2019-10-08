<h1>Como fazer uma API em Node</h1>
<h3>Passo a passo:</h3>

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
