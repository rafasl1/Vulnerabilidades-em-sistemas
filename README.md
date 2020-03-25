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
