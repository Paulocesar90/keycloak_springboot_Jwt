<h1>Integração Keycloak JWT com Spring Boot</h1>

<h2>Clone o Projeto</h2>
<p>Clone o projeto do GitHub para iniciar a integração:</p>
<pre>git clone git@github.com:Paulocesar90/keycloak_springboot_Jwt.git</pre>

<h2>Configuração do Keycloak</h2>
<ul>
    <li><strong>Docker:</strong> Para executar o servidor Keycloak.</li>
    <li><a href="https://www.keycloak.org/getting-started/getting-started-docker" target="_blank">Instalação do Keycloak no Docker</a></li>
</ul>

<p>Execute o seguinte comando Docker para rodar o Keycloak:</p>
<pre>docker run -p 8080:8080 -e KEYCLOAK_ADMIN=admin -e KEYCLOAK_ADMIN_PASSWORD=admin quay.io/keycloak/keycloak:24.0.0 start-dev</pre>

<p>Após a execução, acesse o console do Keycloak em <a href="http://localhost:8080/admin/master/console/" target="_blank">http://localhost:8080/admin/master/console/</a></p>

<p>Crie um novo realm chamado "spring". Em seguida, vá para "Clients", adicione um novo client com o nome "app_spring", e siga as instruções.</p>

<p>Em "Real Roles", adicione duas roles: "ADMIN" e "USER". Em "Users", crie dois usuários, "admin" e "user_test", e atribua as respectivas roles.</p>

<p>Atribua permissões para os usuários:</p>
<ul>
    <li>Para o usuário "admin", atribua a role "ADMIN".</li>
    <li>Para o usuário "user_test", atribua a role "USER".</li>
</ul>

<h2>Testando a Integração</h2>

<p>Abra o Postman e faça uma requisição POST para a URL http://localhost:8081/token/ com o seguinte corpo (JSON) para o usuário "admin":</p>

```json
{
  "clientId": "app_spring",
  "username": "admin",
  "password": "adm",
  "grantType": "password"
}
```


<p>Repita o processo usando o seguinte JSON para o usuário "user_test":</p>

```json
{
  "clientId": "app_spring",
  "username": "user_test",
  "password": "user",
  "grantType": "password"
}
```
<p>Após receber o access_token, abra uma nova requisição POST e utilize a URL http://localhost:8081/products/. No corpo da requisição, coloque o access_token no formato Bearer Token.</p>
<p>Ao enviar a requisição, a resposta será "Cadastrando produtos", confirmando a operação do usuário "admin".</p>
<p>Repita o processo usando o seguinte JSON para o usuário "user_test":</p>
<p>Configure o tipo de requisição para GET e utilize a URL http://localhost:8081/products/.</p>
<p>Ao enviar a requisição, a resposta será "Listando produtos", confirmando a operação do usuário "user_test".</p>




