# Vulnerabilidades-em-sistemas
Esse é um documento para quem quer aprender sobre algumas vulnerabilidades e falhas de segurança básicas em sistemas.
<br> Espero que te ajude a dar um norte no seus estudos de segurança da informação :)

<h2>SQL Injection</h2>
<br><p> O SQL injection nada mais é do que uma injeção de código SQL no seu sistema. Normalmente é feito em campos de input, como em um formulários de login, cadastro ou até mesmo em uma newsletter. Pode ser extremamente perigoso, afinal, se não for evitado pode fazer com que seu banco de dados funcione de forma indesejada.<p>

Exemplo:<br>
Suponha que um usuário mal intencionado (como um hacker) queira acessar o email de outro usuário qualquer. Se o primeiro souber o endereço de email do segundo, isso já é o suficiente para invadir a conta. Isso pode ser feito da seguinte forma: <br>

![login](https://user-images.githubusercontent.com/49666986/77588523-cc666a80-6ec8-11ea-807e-f0356618ecc2.jpg)

No input da senha, está escrito: 
<code>
x’ or ‘a’=’a  
</code>
<br>
Se o sistema estiver usando um banco de dados como mySQL, provavelmente a query que será processada pelo banco será algo parecida com:<br>
<code>
SELECT username FROM accounts WHERE email = ‘fulano@gmail.com’ AND password = ‘ x’ or ‘a’ = ‘a  ’;
</code>

<p>Para que o hacker faça login com sucesso, a segunda cláusula lógica depois do AND deve ser verdadeira. Nesse caso, ele obterá sucesso mesmo com a senha errada, pois:</p>

<code>email = ‘fulano@gmail.com’</code> (isso é verdadeiro) e <code>password = ‘x’ or ‘a’ = ‘a’;</code> (isso é verdadeiro também)<br>

Nesse caso, o hacker conseguirá fazer login na conta do usuário.<br>

Para tratar esse problema em um sistema que usa PHP, uma alternativa é usar a função <code>addSlashes</code>. Ela adiciona barras invertidas a uma string que contenha os caracteres (‘), (“) e (\)  e que são enviadas ao banco de dados, mas a barra invertida não é inserida no banco. <br>
Documentação: https://www.php.net/manual/pt_BR/function.addslashes.php

<h2>Cross Site Scripting (XSS)</h2>

<p>O XSS é uma vulnerabilidade semelhante ao SQL injection, mas usualmente ocorre com uma inserção de código JavaScript e pode fazer com que a página funcione de forma indesejada. Isso pode acontecer de várias formas, desde avisos na tela até páginas em branco ou imagens não desejadas aparecendo na tela.</p>
<p>
Exemplo: 
Suponha que o seu site tenha uma página onde é possível adicionar um comentário sobre um texto que ela acabou de ler (como em um blog). Se um hacker mal intencionado quiser fazer com que a página fique toda em branco, ele pode inserir o código: </p>
<code>
<script>
     document.body.innerHTML = “ ”;
</script></code>

Se ele quiser ser mais criativo, pode colocar uma imagem na página apenas inserindo:
<code>
<script>
     document.body.innerHTML = “ “;<br>
     var imagem = new Image ();<br>
     imagem.src = “[url da imagem]”;<br>
     document.body.appendChild(imagem);<br>
</script></code>
<p>
Isso tudo ocorre porque o Hacker está inserindo códigos JavaScript no corpo do HTML.
Uma forma de evitar esse tipo de ataque é realizar o escaping de elementos HTML. No Java isso pode ser feito através de uma biblioteca chamada ESAPI.</p>
<code>
String encoding=ESAPI.encoder().encodeForJavaScript();</code>
<p>
No PHP, pode-se usar a função htmlspecialchars, que pode fazer com que trechos de códigos JS sejam interpretados como elementos HTML quaisquer.</p>
<p>Documentação: https://www.php.net/manual/pt_BR/function.htmlspecialchars.php</p>


### Vou atualizar isso aqui mais tarde com os outros tópicos (Brute-force, engenharia social e etc). Volte aqui depois pra conferir! :D
