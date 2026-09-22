# Bibliotecas Python

## Pesquisa sobre bibliotecas Python para conexão com bancos de dados

**Alunos:** Emilly Laís Lemke, Giovana de Souza Gomes, Larissa Lemes de Souza, Maria Eduarda Sacavem de Souza e Mateus Tavares dos Santos.

---

# pyodbc

### 1. Qual é o objetivo principal da biblioteca?

O objetivo principal da biblioteca `pyodbc` é oferecer uma interface de banco de dados padronizada e unificada em Python que segue a especificação Python DB API 2.0. Desenvolvida como um módulo open-source, ela opera sobre a camada ODBC (Open Database Connectivity) para permitir que aplicações em Python se comuniquem com diversos sistemas de armazenamento de dados nos sistemas Windows, macOS e Linux (plataformas de 32 e 64 bits) sem a necessidade de grandes alterações no código.

### 2. Que tipo de banco de dados ela permite acessar?

A biblioteca permite acessar uma ampla variedade de bancos de dados relacionais, fontes de dados em nuvem, arquivos e serviços SaaS por meio de drivers ODBC.

Entre as fontes suportadas estão:

- **SGBDs Relacionais:** Microsoft SQL Server, Oracle, MySQL, PostgreSQL, SQLite, Microsoft Access, IBM Netezza, Teradata, Vertica, Sybase ASE e Firebird.
- **Motores de Big Data e Data Warehouses:** Google BigQuery, Amazon Redshift, Snowflake e Apache Hive.
- **Planilhas e Arquivos:** Microsoft Excel e FileMaker Pro.
- **Aplicações em Nuvem / SaaS:** Salesforce, Dynamics 365, Zoho CRM, HubSpot, Mailchimp, entre outros.

### 3. Ela é mais indicada para bancos relacionais ou não relacionais?

A biblioteca é mais indicada para bancos de dados relacionais, uma vez que o padrão ODBC e a especificação DB API 2.0 foram projetados para o envio e manipulação de dados via linguagem SQL.

Embora existam drivers ODBC capazes de conectar a fontes NoSQL, como MongoDB, ou serviços em nuvem traduzindo requisições para a norma ANSI SQL-92, o foco e a aplicação nativa do `pyodbc` permanecem no ecossistema relacional.

### 4. A biblioteca trabalha com SQL puro, ORM ou ambos?

A biblioteca trabalha diretamente com **SQL puro**, atuando como um driver de conexão de baixo nível.

As instruções SQL brutas, como `SELECT`, `INSERT` e `UPDATE`, são enviadas ao banco por meio da função `cursor.execute()`.

O `pyodbc` não é um ORM, mas serve como o driver subjacente sobre o qual frameworks e aplicações executam suas consultas.

### 5. Como é feita a instalação?

A instalação é feita diretamente via gerenciador de pacotes `pip`:

```bash
pip install pyodbc
```

### 6. Como é criado um exemplo simples de conexão?

A conexão é criada chamando a função `pyodbc.connect()` e passando a connection string com o driver ODBC e os parâmetros do banco:

```python
import pyodbc

# Estabelecendo a conexão informando o driver ODBC e o banco
cnxn = pyodbc.connect(
    'DRIVER={Devart ODBC Driver for SQLite};'
    'Direct=True;'
    'Database=mydatabase'
)
```

### 7. Como executar uma consulta SELECT simples?

Para executar uma consulta `SELECT`, cria-se um objeto cursor através da função `cursor()`, executa-se o comando SQL com `execute()` e recuperam-se os registros utilizando `fetchone()`:

```python
import pyodbc

# 1. Criar a conexão com o banco de dados
cnxn = pyodbc.connect(
    'DRIVER={Devart ODBC Driver for SQLite};'
    'Direct=True;'
    'Database=mydatabase'
)

# 2. Criar o objeto cursor
cursor = cnxn.cursor()

# 3. Executar a consulta SELECT em SQL puro
cursor.execute("SELECT * FROM EMP")

# 4. Iterar pelos resultados recuperando linha por linha
row = cursor.fetchone()

while row:
    print(row)
    row = cursor.fetchone()
```

### 8. Vantagens

- **Interface Padronizada (Python DB API 2.0):** implementa a especificação DB API 2.0 e segue o padrão Microsoft ODBC 3.52.
- **Ampla Compatibilidade de Ambientes e Fontes:** funciona em Windows, macOS e Linux e conecta-se a diversos SGBDs, Data Warehouses, planilhas e plataformas SaaS.
- **Alto Desempenho em Operações em Lote:** suporta atualização e inserção de dados em lote, utilizando recursos como `fast_executemany`.
- **Conexões Seguras:** permite proteger os dados em trânsito utilizando criptografia SSL/SSH e tunelamento HTTPS.
- **Mapeamento de Tipos e Suporte a Unicode:** oferece suporte a Unicode e permite mapear tipos de dados SQL específicos para tipos ODBC padrão.
- **Suporte a SQL em Serviços Cloud:** permite executar comandos no padrão ANSI SQL-92 em aplicações SaaS e APIs de nuvem.

### 9. Limitações

- **Dependência de Drivers ODBC Externos:** depende da instalação e configuração prévia dos drivers ODBC específicos do banco.
- **Orientação a SQL e Estruturas Relacionais:** não é nativamente indicado para manipulação direta de bancos NoSQL.
- **Operação em Baixo Nível:** trabalha enviando instruções SQL brutas e manipulando cursores.
- **Variação de Recursos pelo Driver:** funcionalidades avançadas dependem das capacidades oferecidas pelo driver ODBC utilizado.

### 10. Cenários de Uso

- **Aplicações Corporativas Multi-banco:** sistemas em Python que precisam se comunicar com diferentes SGBDs.
- **Pipelines de ETL e Data Warehousing:** processos de ingestão e carga de dados para repositórios analíticos.
- **Integração e Consolidação de Dados SaaS:** extração e automação de relatórios utilizando sintaxe SQL.
- **Desenvolvimento Multiplataforma:** softwares e scripts em Python projetados para Windows, Linux ou macOS.

---

# pymssql

### 1. Qual é o objetivo principal da biblioteca?

O objetivo principal da biblioteca `pymssql` é oferecer uma interface simples e direta de banco de dados em Python que segue a especificação Python DB-API (PEP-249), construída sobre o FreeTDS, para permitir a comunicação e interação de aplicações Python com o Microsoft SQL Server.

### 2. Que tipo de banco de dados ela permite acessar?

A biblioteca permite acessar o banco de dados **Microsoft SQL Server**, incluindo instâncias locais, servidores em rede e serviços baseados em nuvem como o Azure SQL Database.

### 3. Ela é mais indicada para bancos relacionais ou não relacionais?

A biblioteca é indicada para bancos de dados relacionais, já que o Microsoft SQL Server é um sistema gerenciador de banco de dados relacional (RDBMS).

### 4. A biblioteca trabalha com SQL puro, ORM ou ambos?

A biblioteca trabalha nativamente com **SQL puro**, fornecendo a interface padrão DB-API para envio de comandos T-SQL e execução de instruções preparadas.

Além disso, disponibiliza um módulo interno de mais baixo nível chamado `_mssql`.

Embora o `pymssql` não seja um ORM, ele pode ser utilizado por frameworks ORM, como o SQLAlchemy, como driver de conexão subjacente.

### 5. Como é feita a instalação?

A instalação é feita via `pip`. É recomendável atualizar o `pip` antes de instalar:

```bash
pip install -U pip
pip install pymssql
```

> **Nota:** Os wheels oficiais do `pymssql` vêm com uma cópia estática do FreeTDS e suporte a SSL embutido.

### 6. Como é criado um exemplo simples de conexão?

```python
import pymssql

# Definindo os parâmetros de conexão
server = "localhost"
user = "meu_usuario"
password = "minha_senha"
database = "tempdb"

# Estabelecendo a conexão
conn = pymssql.connect(server, user, password, database)
```

### 7. Como executar uma consulta SELECT simples?

```python
import pymssql

# 1. Criar a conexão com o banco de dados
conn = pymssql.connect(
    "localhost",
    "meu_usuario",
    "minha_senha",
    "tempdb"
)

# 2. Criar o cursor
cursor = conn.cursor(as_dict=True)

# 3. Executar o SELECT com consulta parametrizada
cursor.execute(
    'SELECT * FROM persons WHERE salesrep=%s',
    'John Doe'
)

# 4. Iterar pelos resultados
for row in cursor:
    print("ID=%d, Name=%s" % (row['id'], row['name']))

# 5. Fechar a conexão
conn.close()
```

### 8. Vantagens

- **Instalação e Deploy Descomplicados:** os wheels trazem o FreeTDS compilado estaticamente com SSL.
- **Sem Necessidade de Drivers ODBC Proprietários:** permite conexão direta ao banco.
- **Alta Performance:** a implementação em Cython reduz a sobrecarga na comunicação entre Python e C.
- **Compatibilidade com Concorrência Cooperativa:** compatível com frameworks como `gevent`.
- **Conexão com Nuvem (Azure SQL):** permite conectar a instâncias do Azure SQL Database utilizando SSL.

### 9. Limitações

- **Dependência da Arquitetura FreeTDS / DB-Lib:** recursos T-SQL mais recentes podem demorar mais para serem incorporados.
- **Ausência de Mapeamento ORM Nativo:** trabalha exclusivamente com SQL puro.
- **Recursos Avançados Corporativos do Azure:** para recursos como Azure Managed Identity / Entra ID, Always Encrypted ou Apache Arrow, outros drivers podem ser mais adequados.

### 10. Cenários de Uso

- **Aplicações e Microsserviços em Containers:** ambientes isolados onde se deseja um deploy simples.
- **Scripts de Automação e Tarefas de ETL Leves:** scripts rápidos de manutenção e integração de dados.
- **Sistemas Assíncronos / Cooperativos:** aplicações que utilizam bibliotecas como `gevent`.
- **Projetos Legados ou Baseados em Stored Procedures:** sistemas que utilizam consultas T-SQL e stored procedures.

---

# psycopg2

### 1. Qual é o objetivo principal da biblioteca?

O `psycopg2` é um adaptador de banco de dados para conectar aplicações Python ao PostgreSQL.

Ele implementa a especificação completa do Python DB-API 2.0 (PEP 249) e é thread-safe, sendo indicado para aplicações que realizam diversas operações de banco de dados.

### 2. Que tipo de banco de dados ela permite acessar?

O `psycopg2` conecta exclusivamente a bancos **PostgreSQL**, que é um banco de dados relacional.

Diferente do `pymssql`, que utiliza o FreeTDS, o `psycopg2` é implementado majoritariamente em C, como um wrapper da `libpq`, a biblioteca cliente oficial do PostgreSQL.

Ele suporta:

- cursors client-side;
- cursors server-side;
- comunicação assíncrona;
- notificações;
- comandos `COPY TO` e `COPY FROM`.

O `psycopg2` continua sendo amplamente utilizado, porém o desenvolvimento atual está concentrado no **Psycopg 3**, seu sucessor.

### 3. Ela é mais indicada para bancos relacionais ou não relacionais?

É indicada para bancos relacionais, já que o PostgreSQL é um SGBD relacional (RDBMS).

### 4. A biblioteca trabalha com SQL puro, ORM ou ambos?

O `psycopg2` trabalha nativamente com **SQL puro** através da DB-API.

Ele não é um ORM, mas pode ser utilizado como driver de conexão por ferramentas ORM, como SQLAlchemy.

### 5. Como é feita a instalação?

Existem duas opções:

**Versão binária:**

```bash
pip install -U pip
pip install psycopg2-binary
```

**Versão compilada a partir do código-fonte:**

```bash
pip install psycopg2
```

A versão binária é recomendada para desenvolvimento e testes, enquanto a versão compilada pode ser utilizada em produção.

### 6. Como é criado um exemplo simples de conexão?

```python
import psycopg2

conn = psycopg2.connect(
    host="localhost",
    port=5432,
    dbname="tempdb",
    user="meu_usuario",
    password="minha_senha"
)
```

### 7. Como executar uma consulta SELECT simples?

```python
import psycopg2
from psycopg2.extras import RealDictCursor

# 1. Criar a conexão com o banco de dados
conn = psycopg2.connect(
    host="localhost",
    dbname="tempdb",
    user="meu_usuario",
    password="minha_senha"
)

# 2. Criar o cursor
cursor = conn.cursor(cursor_factory=RealDictCursor)

# 3. Executar o SELECT com consulta parametrizada
cursor.execute(
    "SELECT * FROM persons WHERE salesrep = %s",
    ("John Doe",)
)

# 4. Iterar pelos resultados
for row in cursor:
    print(f"ID={row['id']}, Name={row['name']}")

# 5. Fechar cursor e conexão
cursor.close()
conn.close()
```

### 8. Vantagens

- **Integração nativa com PostgreSQL**
- **Boa performance**
- **Suporte a operações avançadas**
- **Integração com ORMs**

### 9. Limitações

- **Exclusivo para PostgreSQL:** desenvolvido especificamente para PostgreSQL.
- **Sem recursos de ORM:** para utilizar ORM é necessário utilizar uma ferramenta adicional.
- **Código mais verboso em aplicações maiores:** exige gerenciamento manual de conexões, cursores, transações e consultas SQL.
- **Não é uma solução de conexão assíncrona moderna:** aplicações que utilizam `asyncio` podem se beneficiar mais diretamente das APIs assíncronas do Psycopg 3.

### 10. Cenários de Uso

- **Aplicações Web:** utilizado como driver de conexão entre aplicações Python e PostgreSQL.
- **APIs e Sistemas Backend:** adequado para operações frequentes de `SELECT`, `INSERT`, `UPDATE` e `DELETE`.
- **Processamento e carga de grandes volumes de dados:** utilização dos comandos `COPY TO` e `COPY FROM`.
- **ETL e integração de dados:** extração, transformação e carregamento de dados.
- **Scripts e automações:** consultas, inserções e atualizações em PostgreSQL.
- **Sistemas que exigem controle de transações:** permite controlar `commit`, `rollback` e isolamento.
- **Aplicações que utilizam ORM:** pode atuar como driver para ferramentas como SQLAlchemy e Django.

---

# SQLAlchemy

### 1. Qual é o objetivo principal da biblioteca?

O SQLAlchemy é uma biblioteca do Python utilizada para trabalhar com bancos de dados relacionais.

Ela facilita a comunicação entre uma aplicação Python e o banco de dados.

Seu principal objetivo é permitir que o desenvolvedor possa conectar, consultar, inserir, atualizar e excluir dados utilizando Python.

O SQLAlchemy também possui recursos que ajudam a evitar a necessidade de escrever todo o SQL manualmente, principalmente através do ORM (Object-Relational Mapping).

### 2. Que tipo de banco de dados ela permite acessar?

O SQLAlchemy permite trabalhar com diversos bancos de dados relacionais, por exemplo:

- MySQL
- PostgreSQL
- SQLite
- Microsoft SQL Server
- Oracle

Para cada banco de dados, normalmente é utilizado um driver específico.

Por exemplo, para SQLite, que já vem integrado ao Python, não é necessário instalar um driver adicional.

### 3. Ela é mais indicada para bancos relacionais ou não relacionais?

O SQLAlchemy é principalmente indicado para bancos de dados relacionais.

Ele foi desenvolvido para trabalhar com conceitos como:

- tabelas;
- colunas;
- registros;
- chaves primárias;
- relacionamentos entre tabelas;
- SQL.

Portanto, não é uma biblioteca voltada diretamente para bancos não relacionais, como MongoDB ou Redis.

### 4. A biblioteca trabalha com SQL puro, ORM ou ambos?

O SQLAlchemy trabalha com **SQL puro e ORM**.

#### SQL

É possível executar comandos SQL diretamente utilizando a biblioteca.

Exemplo:

```python
from sqlalchemy import create_engine, text

engine = create_engine("sqlite:///banco.db")

with engine.connect() as conexao:
    resultado = conexao.execute(
        text("SELECT * FROM usuarios")
    )

    for linha in resultado:
        print(linha)
```

Nesse exemplo, o comando `SELECT` foi escrito diretamente em SQL.

#### ORM

O SQLAlchemy também possui o ORM, que significa **Object-Relational Mapping**.

Com o ORM, tabelas do banco podem ser representadas como classes Python. Dessa forma, o programador pode trabalhar com objetos Python em vez de escrever todos os comandos SQL manualmente.

Exemplo simplificado:

```python
from sqlalchemy.orm import DeclarativeBase, Mapped, mapped_column

class Base(DeclarativeBase):
    pass

class Usuario(Base):
    __tablename__ = "usuarios"

    id: Mapped[int] = mapped_column(primary_key=True)
    nome: Mapped[str]
```

Nesse caso, a tabela `usuarios` é representada pela classe `Usuario`.

### 5. Como é feita a instalação?

A instalação pode ser feita utilizando o `pip`:

```bash
pip install SQLAlchemy
```

Depois da instalação, a biblioteca pode ser importada:

```python
import sqlalchemy
```

Para utilizar determinados bancos de dados, também pode ser necessário instalar o driver correspondente.

Por exemplo, para PostgreSQL:

```bash
pip install psycopg2-binary
```

### 6. Como é criado um exemplo simples de conexão?

Para criar uma conexão, primeiro é necessário criar um `engine`.

O `engine` é responsável por gerenciar a comunicação entre o programa e o banco de dados.

Exemplo utilizando SQLite:

```python
from sqlalchemy import create_engine

engine = create_engine("sqlite:///banco.db")

with engine.connect() as conexao:
    print("Conexão realizada com sucesso!")
```

Nesse exemplo:

- `create_engine()` cria o mecanismo de conexão;
- `"sqlite:///banco.db"` indica que será utilizado um banco SQLite chamado `banco.db`;
- `engine.connect()` realiza a conexão;
- `with` garante que a conexão seja encerrada corretamente depois do uso.

### 7. Como executar uma consulta SELECT simples?

Para executar um `SELECT`, podemos utilizar a função `text()` do SQLAlchemy.

```python
from sqlalchemy import create_engine, text

engine = create_engine("sqlite:///banco.db")

with engine.connect() as conexao:
    resultado = conexao.execute(
        text("SELECT * FROM usuarios")
    )

    for usuario in resultado:
        print(usuario)
```

O comando:

```sql
SELECT * FROM usuarios
```

significa que queremos selecionar todos os dados da tabela `usuarios`.

Também podemos selecionar apenas algumas colunas:

```python
from sqlalchemy import create_engine, text

engine = create_engine("sqlite:///banco.db")

with engine.connect() as conexao:
    resultado = conexao.execute(
        text("SELECT id, nome FROM usuarios")
    )

    for usuario in resultado:
        print(usuario.id, usuario.nome)
```

Nesse caso, serão retornados apenas os campos `id` e `nome`.

### Exemplo completo

Abaixo está um exemplo simples reunindo a conexão e a consulta `SELECT`:

```python
from sqlalchemy import create_engine, text

engine = create_engine("sqlite:///banco.db")

with engine.connect() as conexao:
    resultado = conexao.execute(
        text("SELECT id, nome FROM usuarios")
    )

    for usuario in resultado:
        print(f"ID: {usuario.id} - Nome: {usuario.nome}")
```

Esse código cria uma conexão com o banco `banco.db`, executa uma consulta na tabela `usuarios` e mostra o `id` e o nome de cada usuário encontrado.

### 8. Vantagens

- **Flexibilidade e controle:** permite transitar entre ORM e consultas SQL puras ou de baixo nível (Core).
- **Abstração de banco de dados:** permite trabalhar com diferentes sistemas de banco de dados alterando a string de conexão.
- **Prevenção contra SQL Injection:** utiliza consultas parametrizadas (bound parameters).
- **Gerenciamento avançado de sessões:** utiliza o padrão Unit of Work.
- **Ecossistema maduro:** integra-se com frameworks como Flask, FastAPI e Alembic.

### 9. Limitações

- **Curva de aprendizado:** possui uma API complexa para iniciantes.
- **Sobrecarga de performance (Overhead):** o mapeamento de linhas para objetos Python pode consumir mais memória e processamento.
- **Complexidade em queries gigantes:** consultas muito complexas podem ser mais confusas utilizando ORM.
- **Configuração manual:** conexão, sessões e ferramentas de migração precisam ser configuradas.

### 10. Cenários de Uso

- **Aplicações Enterprise ou Complexas:** projetos com regras de negócio e relacionamentos complexos.
- **APIs com Flask ou FastAPI:** APIs modernas com alta customização.
- **Sistemas Multi-banco de dados:** projetos que utilizam diferentes bancos em diferentes ambientes.
- **Migração Gradual de Código:** bancos legados que precisam ser mapeados aos poucos.

---

# sqlite3

### 1. Qual é o objetivo principal da biblioteca?

O objetivo principal do módulo `sqlite3` é fornecer uma interface SQL padronizada e compatível com a especificação DB-API 2.0 (PEP 249) em Python.

Ele permite que aplicações criem, conectem, consultem e gerenciem bancos de dados SQLite diretamente no código, sem a necessidade de administrar um servidor de banco de dados independente.

### 2. Que tipo de banco de dados ela permite acessar?

Ela permite acessar o **SQLite**, que é um sistema de gerenciamento de banco de dados:

- embutido (embedded);
- autocontido (self-contained);
- de configuração zero (zero-configuration);
- sem servidor (serverless).

Ele armazena as tabelas e dados diretamente em um único arquivo de disco ou temporariamente na memória RAM.

### 3. Ela é mais indicada para bancos relacionais ou não relacionais?

A biblioteca é indicada para bancos de dados relacionais.

O SQLite opera com o modelo relacional baseado em SQL, oferecendo suporte a:

- tabelas;
- transações com propriedades ACID;
- chaves primárias e estrangeiras;
- subconsultas;
- junções (`JOINs`).

### 4. A biblioteca trabalha com SQL puro, ORM ou ambos?

A biblioteca `sqlite3` trabalha nativamente com **SQL puro**.

A comunicação com o banco é feita enviando instruções SQL diretamente na forma de strings através de métodos como:

- `cursor.execute()`;
- `executemany()`;
- `executescript()`.

Ferramentas de ORM de terceiros, como SQLAlchemy, podem utilizar a biblioteca `sqlite3` como driver de conexão.

### 5. Como é feita a instalação?

Não é necessário instalar nada.

O módulo `sqlite3` já vem integrado à biblioteca padrão da linguagem Python.

Para utilizá-lo, basta incluir:

```python
import sqlite3
```

### 6. Como é criado um exemplo simples de conexão?

A conexão é criada chamando a função `sqlite3.connect()`, passando o caminho do arquivo do banco de dados.

Se o arquivo não existir, ele será criado automaticamente.

```python
import sqlite3

# 1. Estabelece a conexão com o arquivo de banco de dados
conexao = sqlite3.connect("meu_banco.db")

# 2. Cria o objeto cursor para enviar comandos SQL
cursor = conexao.cursor()

print("Conexão estabelecida com sucesso!")

# 3. Fecha a conexão ao finalizar
conexao.close()
```

### 7. Como executar uma consulta SELECT simples?

Para executar uma consulta `SELECT`, utiliza-se o método `cursor.execute()` com a instrução SQL desejada.

Os dados podem ser obtidos utilizando métodos como `fetchall()`, `fetchone()` ou iterando diretamente sobre o cursor.

```python
import sqlite3

# Conecta ao banco de dados e cria o cursor
conexao = sqlite3.connect("meu_banco.db")
cursor = conexao.cursor()

# Cria a tabela e insere dados de exemplo para o teste
cursor.execute(
    "CREATE TABLE IF NOT EXISTS usuarios "
    "(id INTEGER PRIMARY KEY, nome TEXT)"
)

cursor.execute(
    "INSERT INTO usuarios (nome) VALUES ('Ana'), ('Carlos')"
)

conexao.commit()

# Executa a consulta SELECT simples
cursor.execute("SELECT id, nome FROM usuarios")

# Recuperando todos os registros com fetchall()
resultados = cursor.fetchall()

for linha in resultados:
    print(f"ID: {linha[0]}, Nome: {linha[1]}")

# Fecha a conexão
conexao.close()
```

### 8. Vantagens

- **Módulo Nativo (Zero Instalação):** já vem integrado à biblioteca padrão do Python.
- **Arquitetura Serverless e Zero Configuração:** não exige instalação ou execução de um servidor separado.
- **Autocontido e Leve:** todo o banco de dados é armazenado em um único arquivo ou na memória RAM.
- **Suporte Transacional ACID:** oferece suporte a transações.
- **Portabilidade (Cross-platform):** os arquivos `.db` ou `.sqlite` podem ser utilizados em diferentes sistemas operacionais.
- **Segurança na Aplicação:** suporta placeholders (`?` ou `:nome`) para prevenir ataques de SQL Injection.

### 9. Limitações

- **Sem Acesso Direto via Rede:** não oferece suporte nativo para conexões diretas através de redes.
- **Ausência de Autenticação e Controle de Usuários:** não possui sistema interno para criação de usuários, senhas ou permissões específicas.
- **Concorrência de Escrita Limitada:** não é adequado para alta taxa de operações de escrita simultâneas.
- **Restrição de Escala e Replicação:** não foi projetado para grandes volumetrias de dados ou replicação distribuída entre múltiplos servidores.

### 10. Cenários de Uso

- **Aplicações Móveis e Desktop:** armazenamento interno em aplicativos e softwares locais.
- **Sistemas Embarcados e IoT:** dispositivos com recursos limitados de hardware.
- **Prototipagem Rápida e Testes:** criação de protótipos e testes automatizados.
- **Armazenamento de Configurações e Cache Local:** armazenamento de preferências, logs e dados em cache.
- **Aplicações Web de Baixo e Médio Tráfego:** sites e ferramentas internas com predominância de consultas.
