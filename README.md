# MySql - All for One

# Contexto
O `All for One` é um conjunto de Comandos em MySql para resolver desafios! <br>
Possui 27 desafios como Filtragem de dados, Manipulação de tabelas, Exibir e puxar informações específicas.

# Orientações

<details>
  <summary><strong>:whale: Rodando no Docker</strong></summary><br />

  ## Com Docker

  **:warning: Antes de começar, seu docker-compose precisa estar na versão 1.29 ou superior. [Veja aqui](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-compose-on-ubuntu-20-04-pt) ou [na documentação](https://docs.docker.com/compose/install/) como instalá-lo. No primeiro artigo, você pode substituir onde está com `1.26.0` por `1.29.2`.**

  > :information_source: Rode os serviços `node` e `db` com o comando `docker-compose up -d`.
  - Lembre-se de parar o `mysql` se estiver usando localmente na porta padrão (`3306`), ou adapte, caso queria fazer uso da aplicação em containers
  - Esses serviços irão inicializar um container chamado `all_for_one` e outro chamado `all_for_one_db`.
  - A partir daqui você pode rodar o container `all_for_one` via CLI ou abri-lo no VS Code.

  > :information_source: Use o comando `docker exec -it all_for_one bash`.
  - Ele te dará acesso ao terminal interativo do container criado pelo compose, que está rodando em segundo plano.
  - As credencias de acesso ao banco de dados estão definidas no arquivo `docker-compose.yml`, e são acessíveis no container através das variáveis de ambiente `MYSQL_USER` e `MYSQL_PASSWORD`. 💡

  > :information_source: Instale as dependências com `npm install`. (Instale dentro do container)

  - **:warning: Atenção:** Caso opte por utilizar o Docker, **TODOS** os comandos disponíveis no `package.json` (npm start, npm test, npm run dev, ...) devem ser executados **DENTRO** do container, ou seja, no terminal que aparece após a execução do comando `docker exec` citado acima.

  - **:warning: Atenção:** O **git** dentro do container não vem configurado com suas credenciais. Ou faça os commits fora do container, ou configure as suas credenciais do git dentro do container.

  - **:warning: Atenção:** Não rode o comando npm audit fix! Ele atualiza várias dependências do projeto.

  <br />
</details>

<details>
  <summary><strong>🗒️ Instruções para restaurar o banco de dados `Northwind`</strong></summary><br />

1. Faça o download do arquivo de backup [aqui](northwind.sql) clicando em "Raw", depois clicando com botão direito e selecionando "Salvar como" para salvar o arquivo em seu computador.
2. Abra o arquivo com algum editor de texto e selecione todo o conteúdo do arquivo usando `CTRL-A`.
3. Abra o MySQL Workbench.
4. Abra uma nova janela de query e cole dentro dela todo o conteúdo do arquivo `northwind.sql`.
5. Selecione todo o código com o atalho `CTRL-A` e depois clique no ícone de raio para executar a query.

    ![Restaurando o banco Northwind](images/restore_northwind.png)
6. Aguarde alguns segundos (espere em torno de 30 segundos antes de tentar fazer algo).
7. Clique no botão apontado na imagem a seguir para atualizar a listagem de banco de dados.

    ![Tabelas do banco Northwind](images/refresh_databases.png)
7. Verifique se o banco restaurado possui todas as seguintes tabelas:

    ![Tabelas do banco Northwind](images/northwind.png)
8. Clique com botão direito em cada tabela e selecione "Select Rows" e certifique-se que todas as tabelas possuem registros. Caso tenha alguma faltando, faça o passo a seguir. Caso contrário, pode ir para próxima seção.
9. Caso existam tabelas faltando, drope o banco de dados clicando com o botão direito em cima do banco de dados northwind e selecionando "Drop Schema" e refaça os passos novamente, dessa vez aguardando um tempo maior quando executar o script de restauração.

    ![Drop Schema](images/drop_database.png)

</details>


<details>
  <summary><strong>📑 Instruções para testar suas queries</strong></summary><br />

#### Para executar os testes locais com Docker 🐋

- Após ter seguido os passos anteriores do `docker-compose up -d` e `docker exec -it all_for_one bash`, dentro do terminal interativo do container, rode:
```sh
npm test
```

#### Para executar os testes locais usando a instalação do MySQL feita na sua máquina 💻

- Para executar localmente os testes é preciso escrever o seguinte no seu terminal:
```sh
MYSQL_USER=<SEU_NOME_DE_PESSOA_USUARIA> MYSQL_PASSWORD=<SUA SENHA> HOSTNAME=<NOME_DO_HOST> PORT=<PORTA> npm test
```

- Não esqueça de substituir os locais indicados com `< >` por suas credenciais:
```sh
MYSQL_USER=root MYSQL_PASSWORD=password HOSTNAME=localhost PORT=3306 npm test
```

#### Dicas e pontos de atenção

- ✨ **Dica:** variáveis de ambiente definidas na mesma linha do comando valem apenas para aquele comando. Se preferir, você pode exportar as variáveis de ambiente para toda a _sessão_ (todos os comandos até você fechar aquele terminal). Por exemplo:
```sh
export MYSQL_USER=root MYSQL_PASSWORD=password HOSTNAME=localhost PORT=3306
```
> E depois disso você só precisa rodar `npm test` quando for testar os projetos.

- ✨ **Dica:** Caso queira utilizar _Docker_ para rodar os testes localmente, basta executar o comando:
```sh
docker run -p 3306:3306 --name mysql_57 -e MYSQL_ROOT_PASSWORD=1234 -d mysql:5.7 mysqld --default-authentication-plugin=mysql_native_password
```
- Depois de usar o comando acima, agora basta executar os testes digitando no terminal:
```sh
MYSQL_USER=root MYSQL_PASSWORD=1234 HOSTNAME=localhost npm test
```
</details>

## Desafios
<details>
1 - Exiba apenas os nomes dos produtos na tabela `products`.

  ---

2 - Exiba os dados de todas as colunas da tabela `products`.

  ---

3 - Escreva uma query que exiba os valores da coluna que representa a primary key da tabela `products`.

  ---

4 - Conte quantos registros existem na coluna `product_name` da tabela `products`.

  ---

5 - Monte uma query que exiba os dados da tabela `products` a partir do quarto registro até o décimo terceiro.

  - Tanto o quarto quanto o décimo terceiro registros, precisam aparecer na consulta;

  - Não use `where` ou `order by`.

  <br />

  ---

6 - Exiba os dados das colunas `product_name` e `id` da tabela `products` de maneira que os resultados estejam em ordem alfabética dos nomes.

  ---

7 - Mostre apenas os ids dos 5 últimos registros da tabela `products` (a ordernação deve ser baseada na coluna `id`).

  ---

8 - Faça uma consulta que retorne três colunas, respectivamente, com os nomes 'A', 'Trybe' e 'eh', e com valores referentes a soma de '5 + 6', a string 'de', a soma de '2 + 8'.


  - Na primeira coluna, exiba a soma de `5 + 6` (essa soma deve ser realizada pelo SQL);

  - Na segunda coluna deve haver a palavra \"de\";

  - E por fim, na terceira coluna, exiba a soma de `2 + 8` (essa soma deve ser realizada pelo SQL);

  - A primeira coluna deve se chamar \"A\", a segunda coluna deve se chamar \"Trybe\" e a terceira coluna deve se chamar \"eh\";

  - Não use colunas pré-existentes, apenas o que for criado na hora.

  <br />

## Desafios sobre filtragem de dados

9 - Mostre todos os valores de `notes` da tabela `purchase_orders` que não são nulos.

  ---

10 - Mostre todos os dados da tabela `purchase_orders` em ordem decrescente, ordenados por `created_by` em que o `created_by` é maior ou igual a 3.


  - Como critério de desempate para a ordenação, ordene também os resultados pelo `id` de forma crescente.

  <br />

  ---

11 - Exiba os dados da coluna `notes` da tabela `purchase_orders` em que seu valor de `Purchase generated based on Order` é maior ou igual a 30 e menor ou igual a 39.

  ---

12 - Mostre as `submitted_date` de `purchase_orders` em que a `submitted_date` é do dia 26 de abril de 2006.

  ---

13 - Mostre o `supplier_id` das `purchase_orders` em que o `supplier_id` seja 1 ou 3.

  ---

14 - Mostre os resultados da coluna `supplier_id` da tabela `purchase_orders` em que o `supplier_id` seja maior ou igual a 1 e menor ou igual 3.

  ---

15 - Mostre somente as horas (sem os minutos e os segundos) da coluna `submitted_date` de todos registros da tabela `purchase_orders`.


  - Chame essa coluna de `submitted_hour`.

  <br />

  ---

16 - Exiba a `submitted_date` das `purchase_orders` que estão entre `2006-01-26 00:00:00` e `2006-03-31 23:59:59`.

  ---

17 - Mostre os registros das colunas `id` e `supplier_id` das `purchase_orders` em que os `supplier_id` sejam tanto 1, ou 3, ou 5, ou 7.

  ---

18 - Mostre todos os registros de `purchase_orders` que tem o `supplier_id` igual a 3 e `status_id` igual a 2.

  ---

19 - Mostre a quantidade de pedidos que foram feitos na tabela `orders` pelo `employee_id` igual a 5 ou 6, e que foram enviados através do método(coluna) `shipper_id` igual a 2.


  - Chame a coluna de `orders_count`.

  <br />

  ---

## Desafios de manipulação de tabelas

20 - Adicione à tabela `order_details` um registro com `order_id`: 69, `product_id`: 80, `quantity`: 15.0000, `unit_price`: 15.0000, `discount`: 0, `status_id`: 2, `date_allocated`: NULL, `purchase_order_id`: NULL e `inventory_id`: 129.


  - Obs.: o `id` deve ser incrementado automaticamente.

  <br />

  ---

21 - Adicione com um único `INSERT`, duas linhas à tabela `order_details` com os mesmos dados do requisito 20.


  - Esses dados são novamente `order_id`: 69, `product_id`: 80, `quantity`: 15.0000, `unit_price`: 15.0000, `discount`: 0, `status_id`: 2, `date_allocated`: NULL, `purchase_order_id`: NULL e `inventory_id`: 129;

  - O `ìd` deve ser incrementado automaticamente.

  <br />

  ---

22 - Atualize os dados de `discount` do `order_details` para 15. (Não é necessário utilizar o SAFE UPDATE em sua query).

  ---

23 - Atualize os dados da coluna `discount` da tabela `order_details` para 30, onde o valor na coluna `unit_price` seja menor que 10.0000.


  - Não é necessário utilizar o SAFE UPDATE em sua query.

  <br />

  ---

24 - Atualize os dados da coluna `discount` da tabela `order_details` para 45, onde o valor na coluna `unit_price` seja maior que 10.0000 e o id seja um número entre 30 e 40.



  - Não é necessário utilizar o SAFE UPDATE em sua query.

  <br />

  ---

25 - Delete todos os dados em que a `unit_price` da tabela `order_details` seja menor que 10.0000.

  ---

26 - Delete todos os dados em que a `unit_price` da tabela `order_details` seja maior que 10.0000.

  ---

27 - Delete todos os dados da tabela `order_details`.

---
</details>
