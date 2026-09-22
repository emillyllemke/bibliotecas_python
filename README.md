# Bibliotecas Python
Pesquisa sobre bibliotecas Python para conexão com bancos de dados
Alunos: Emilly Laís Lemke, Giovana de Souza Gomes, Larissa Lemes de Souza, Maria Eduarda Sacavem de Souza.

# pyodbc
1- O objetivo principal da biblioteca pyodbc é oferecer uma interface de banco de dados padronizada e unificada em Python que segue a especificação Python DB API 2.0. Desenvolvida como um módulo open-source, ela opera sobre a camada ODBC (Open Database Connectivity) para permitir que aplicações em Python se comuniquem com diversos sistemas de armazenamento de dados nos sistemas Windows, macOS e Linux (plataformas de 32 e 64 bits) sem a necessidade de grandes alterações no código.

2- A biblioteca permite acessar uma ampla variedade de bancos de dados relacionais, fontes de dados em nuvem, arquivos e serviços SaaS por meio de drivers ODBC. Entre as fontes suportadas estão:
SGBDs Relacionais: Microsoft SQL Server, Oracle, MySQL, PostgreSQL, SQLite, Microsoft Access, IBM Netezza, Teradata, Vertica, Sybase ASE e Firebird.
Motores de Big Data e Data Warehouses: Google BigQuery, Amazon Redshift, Snowflake e Apache Hive.
Planilhas e Arquivos: Microsoft Excel e FileMaker Pro.
Aplicações em Nuvem / SaaS (com mapeamento via drivers ODBC): Salesforce, Dynamics 365, Zoho CRM, HubSpot, Mailchimp, entre outros.

3- A biblioteca é mais indicada para bancos de dados relacionais, uma vez que o padrão ODBC e a especificação DB API 2.0 foram projetados para o envio e manipulação de dados via linguagem SQL. Embora existam drivers ODBC capazes de conectar a fontes NoSQL (como MongoDB) ou serviços em nuvem traduzindo requisições para a norma ANSI SQL-92, o foco e a aplicação nativa do pyodbc permanecem no ecossistema relacional.

4- A biblioteca trabalha diretamente com SQL puro, atuando como um driver de conexão de baixo nível. As instruções SQL brutas (como SELECT, INSERT, UPDATE) são enviadas ao banco por meio da função cursor.execute(). O pyodbc não é um ORM, mas serve como o driver subjacente sobre o qual frameworks e aplicações executam suas consultas.

5- A instalação é feita diretamente via gerenciador de pacotes pip:
pip install pyodbc

6- A conexão é criada chamando a função pyodbc.connect() e passando a connection string com o driver ODBC e os parâmetros do banco:
import pyodbc
#Estabelecendo a conexão informando o driver ODBC e o banco de dados
cnxn = pyodbc.connect('DRIVER={Devart ODBC Driver for SQLite};Direct=True;Database=mydatabase')

7- Para executar uma consulta SELECT, cria-se um objeto cursor através da função cursor(), executa-se o comando SQL com execute() e recupera-se os registros iterando com a função fetchone():
import pyodbc
#1. Criar a conexão com o banco de dados
cnxn = pyodbc.connect('DRIVER={Devart ODBC Driver for SQLite};Direct=True;Database=mydatabase')
#2. Criar o objeto cursor
cursor = cnxn.cursor()
#3. Executar a consulta SELECT em SQL puro
cursor.execute("SELECT * FROM EMP")
#4. Iterar pelos resultados recuperando linha por linha
row = cursor.fetchone()
while row:
    print(row)
    row = cursor.fetchone()

8- Vantagens
Interface Padronizada (Python DB API 2.0): O pyodbc implementa a especificação DB API 2.0 e segue o padrão Microsoft ODBC 3.52. Isso permite desenvolver aplicações capazes de interagir com diferentes fontes de dados mantendo uma interface de código unificada.
Ampla Compatibilidade de Ambientes e Fontes: Funciona em sistemas Windows, macOS e Linux (32 e 64 bits) e conecta-se a SGBDs relacionais corporativos (SQL Server, Oracle, PostgreSQL, MySQL), Data Warehouses (Snowflake, BigQuery, Redshift), planilhas e plataformas SaaS em nuvem (Salesforce, Zoho CRM, Dynamics 365).
Alto Desempenho em Operações em Lote: Suporta atualização e inserção de dados em lote (via recurso como fast_executemany e instruções unificadas em massa), reduzindo o tempo de execução em comparação com processamentos linha por linha.
Conexões Seguras: Permite proteger os dados em trânsito utilizando criptografia SSL/SSH e tunelamento HTTPS entre a aplicação Python e o servidor remoto ou serviço em nuvem.
Mapeamento de Tipos e Suporte a Unicode: Oferece suporte completo a Unicode e permite mapear tipos de dados SQL específicos de cada fonte para os tipos ODBC padrão.
Suporte a SQL em Serviços Cloud: Permite executar comandos no padrão ANSI SQL-92 em aplicações SaaS e APIs de nuvem que nativamente não possuem suporte direto a SQL.

9- Limitações
Dependência de Drivers ODBC Externos: O pyodbc depende diretamente da instalação e configuração prévia dos drivers ODBC específicos do banco e dos gerenciadores de driver (como o unixODBC no Linux/macOS) no sistema operacional.
Orientação a SQL e Estruturas Relacionais: Por seguir a especificação DB API 2.0 e o protocolo ODBC baseados em SQL, não é nativamente indicado para manipulação direta de bancos NoSQL ou dados não estruturados sem uma camada/driver de tradução SQL intermediária.
Operação em Baixo Nível: Funciona enviando instruções SQL brutas e manipulando cursores. A biblioteca não possui abstrações nativas de ORM (Mapeamento Objeto-Relacional), necessitando de frameworks externos (como SQLAlchemy) caso se deseje trabalhar nesse nível.
Variação de Recursos pelo Driver: Funcionalidades avançadas ou otimizações de desempenho (como o suporte ao fast_executemany) dependem das capacidades oferecidas pelo driver ODBC específico que foi instalado.

10- Cenários de Uso
Aplicações Corporativas Multi-banco: Sistemas em Python que precisam se comunicar simultaneamente com diferentes SGBDs (ex.: SQL Server no ambiente local e PostgreSQL na nuvem) sem duplicar a lógica de acesso.
Pipelines de ETL e Data Warehousing: Processos de ingestão e carga pesada de dados para repositórios analíticos (como Snowflake, BigQuery e Redshift) aproveitando o suporte a execução em lote.
Integração e Consolidação de Dados SaaS: Extração e automação de relatórios unificando dados de sistemas de CRM, Vendas e Marketing (como Salesforce, HubSpot e Zoho CRM) utilizando sintaxe SQL.
Desenvolvimento Multiplataforma: Softwares e scripts em Python projetados para rodar de maneira consistente em ambientes Windows, Linux ou macOS.

 
# pymssql
1- O objetivo principal da biblioteca pymssql é oferecer uma interface simples e direta de banco de dados em Python que segue a especificação Python DB-API (PEP-249), construída sobre o FreeTDS, para permitir a comunicação e interação de aplicações Python com o Microsoft SQL Server.

2- A biblioteca permite acessar o banco de dados Microsoft SQL Server (incluindo instâncias locais, servidores em rede e serviços baseados em nuvem como o Azure SQL Database).

3- A biblioteca é indicada para bancos de dados relacionais, já que o Microsoft SQL Server é um sistema gerenciador de banco de dados relacional (RDBMS).

4- A biblioteca trabalha nativamente com SQL puro, fornecendo a interface padrão DB-API para envio de comandos T-SQL e execução de instruções preparadas. Além disso, ela disponibiliza um módulo interno de mais baixo nível chamado _mssql. Embora o pymssql em si não seja um ORM, ele é frequentemente utilizado por frameworks ORM (como o SQLAlchemy) como o driver de conexão subjacente para executar as consultas no banco.

5- A instalação é feita via pip. É recomendável atualizar o pip antes de instalar para garantir o suporte adequado aos pacotes pré-compilados (wheels): 
pip install -U pip 
pip install pymssql 
Nota: Os wheels oficiais do pymssql vêm com uma cópia estática do FreeTDS e suporte a SSL embutido.

6- A conexão é criada chamando a função pymssql.connect() e passando os parâmetros de acesso ao servidor:
import pymssql 
#Definindo os parâmetros de conexão 
server = "localhost" 
user = "meu_usuario" 
password = "minha_senha" 
database = "tempdb" 
#Estabelecendo a conexão 
conn = pymssql.connect(server, user, password, database) 

7- Para executar uma consulta SELECT, cria-se um objeto cursor, executa-se o comando parametrizado e itera-se sobre os resultados. O parâmetro as_dict=True permite retornar as linhas como dicionários:
import pymssql
#1. Criar a conexão com o banco de dados
conn = pymssql.connect("localhost", "meu_usuario", "minha_senha", "tempdb")
#2. Criar o cursor (retornando as linhas em formato de dicionário)
cursor = conn.cursor(as_dict=True)
#3. Executar o SELECT com consulta parametrizada (%s)
cursor.execute('SELECT * FROM persons WHERE salesrep=%s', 'John Doe')
#4. Iterar pelos resultados
for row in cursor:
    print("ID=%d, Name=%s" % (row['id'], row['name']))
#5. Fechar a conexão ao finalizar
conn.close()

8- Vantagens
Instalação e Deploy Descomplicados: Como os wheels trazem o FreeTDS compilado estaticamente com SSL, não é necessário configurar gerenciadores de drivers ODBC externos no sistema operacional.
Sem Necessidade de Drivers ODBC Proprietários: Permite conexão direta ao banco sem depender do Microsoft ODBC Driver ou de utilitários como o unixODBC.
Alta Performance: A implementação em Cython reduz drasticamente a sobrecarga na comunicação entre o código Python e a biblioteca em C.
Compatibilidade com Concorrência Cooperativa: É compatível com frameworks de I/O não bloqueador e multitarefa cooperativa, como o gevent.
Conexão com Nuvem (Azure SQL): Permite conectar a instâncias do Azure SQL Database utilizando conexões criptografadas por SSL.

9- Limitações
Dependência da Arquitetura FreeTDS / DB-Lib: Por se basear na biblioteca FreeTDS, o suporte a recursos T-SQL mais recentes ou específicos lançados nas versões mais novas do SQL Server pode demorar mais para ser incorporado quando comparado a drivers nativos.
Ausência de Mapeamento ORM Nativo: Trabalha exclusivamente com SQL puro. Para trabalhar com orientação a objetos/ORM, deve ser integrada a uma biblioteca externa, como o SQLAlchemy.
Recursos Avançados Corporativos do Azure: Para recursos avançados de autenticação sem senha (como Azure Managed Identity / Entra ID, Always Encrypted ou integração com Apache Arrow), drivers mais recentes desenvolvidos pela Microsoft (como o mssql-python) costumam ser os mais indicados.

10- Cenários de Uso
Aplicações e Microsserviços em Containers (Docker/Linux): Ideal para ambientes isolados onde se deseja um deploy simples em Python sem precisar instalar dependências de sistema ou pacotes ODBC adicionais na imagem.
Scripts de Automação e Tarefas de ETL Leves: Excelente para scripts rápidos de manutenção, automação ou integração de dados que executam comandos T-SQL diretamente.
Sistemas Assíncronos / Cooperativos: Indicado para aplicações web com alta concorrência que utilizam bibliotecas como gevent.
Projetos Legados ou Baseados em Stored Procedures: Adequado para aplicações que dependem fortemente do uso direto de consultas T-SQL e stored procedures.


# psycopg2
1- psycopg2 é o adaptador de banco de dados mais usado para conectar aplicações Python ao PostgreSQL. Ele implementa a especificação completa do Python DB-API 2.0 (PEP 249) e é thread-safe (várias threads podem compartilhar a mesma conexão), sendo indicado para aplicações que abrem muitos cursors e fazem várias operações concorrentes de INSERT/UPDATE.

2- Diferente do pymssql (que usa o FreeTDS por baixo), o psycopg2 é implementado majoritariamente em C, como um wrapper da libpq (a biblioteca cliente oficial do PostgreSQL) o que o torna eficiente e seguro. Ele suporta cursors client-side e server-side, comunicação assíncrona e notificações, e o comando COPY TO/COPY FROM para carga rápida de dados. O psycopg2 ainda é amplamente usado e mantido, mas não recebe mais novas funcionalidades. O desenvolvimento atual está concentrado no psycopg 3, sucessor da biblioteca.

3- O psycopg2 conecta exclusivamente a bancos PostgreSQL (banco de dados relacional).

4- É indicada para bancos relacionais, já que o PostgreSQL é um SGBD relacional (RDBMS). Como o SQL Server no caso do pymssql. O psycopg2 trabalha nativamente com SQL puro via DB-API (não é um ORM). Porém, assim como o pymssql, ele é muito usado como driver de conexão por baixo de ORMs.

5- A instalação é feita via pip. Existem duas opções:
#Versão binária (recomendada para desenvolvimento/testes — não exige compilador C) 
pip install -U pip 
pip install psycopg2-binary 
#Versão compilada a partir do código-fonte (recomendada para produção — exige compilador C e headers do PostgreSQL) 
pip install psycopg2 

6- Exemplo simples de conexão:
import psycopg2
conn = psycopg2.connect(
    host="localhost",
    port=5432,
    dbname="tempdb",
    user="meu_usuario",
    password="minha_senha"
)

7- Exemplo de consulta SELECT
import psycopg2
from psycopg2.extras import RealDictCursor
#1. Criar a conexão com o banco de dados
conn = psycopg2.connect(
    host="localhost",
    dbname="tempdb",
    user="meu_usuario",
    password="minha_senha"
)
#2. Criar o cursor (retornando as linhas em formato de dicionário)
cursor = conn.cursor(cursor_factory=RealDictCursor)
#3. Executar o SELECT com consulta parametrizada (%s)
cursor.execute("SELECT * FROM persons WHERE salesrep = %s", ("John Doe",))
#4. Iterar pelos resultados
for row in cursor:
    print(f"ID={row['id']}, Name={row['name']}")
#5. Fechar cursor e conexão ao finalizar
cursor.close()
conn.close()

8- Vantagens:
Integração nativa com PostgreSQL
Boa performance 
Suporte a operações avançadas 
Integração com ORMs 

9-Limitações:
Exclusivo para PostgreSQL: o psycopg2 foi desenvolvido especificamente para PostgreSQL.
Sem recursos de ORM: trabalha diretamente com SQL e a API DB-API 2.0. Para utilizar recursos de ORM, é necessário utilizar uma ferramenta adicional, como SQLAlchemy ou Django ORM. 
Código mais verboso em aplicações maiores: quando utilizado diretamente, é necessário gerenciar conexões, cursores, transações e consultas SQL manualmente.
Não é uma solução de conexão assíncrona moderna: apesar de possuir mecanismos de comunicação assíncrona, aplicações modernas que utilizam asyncio podem se beneficiar mais diretamente das APIs assíncronas disponíveis no Psycopg 3.  

10- Cenários de Uso:
Aplicações web: utilizado como driver de conexão entre aplicações Python e bancos PostgreSQL, inclusive como camada inferior de frameworks e ORMs.
APIs e sistemas backend: adequado para aplicações que realizam operações frequentes de SELECT, INSERT, UPDATE e DELETE.
Processamento e carga de grandes volumes de dados: os comandos COPY TO e COPY FROM podem ser utilizados para transferir grandes quantidades de dados de forma eficiente.
ETL e integração de dados: pode ser utilizado em processos que extraem dados de uma fonte, transformam essas informações e carregam os resultados em um banco PostgreSQL.
Scripts e automações: é uma opção prática para scripts Python que precisam consultar, inserir ou atualizar dados em PostgreSQL.
Sistemas que exigem controle de transações: aplicações que precisam controlar explicitamente commit, rollback e o isolamento das operações podem utilizar diretamente os recursos oferecidos pelo driver.
Aplicações que utilizam ORM: pode atuar como driver de banco por baixo de ferramentas como SQLAlchemy e Django, permitindo que essas ferramentas se comuniquem com o PostgreSQL.


# SQLAlchemy
1- Qual é o objetivo principal da biblioteca?
O SQLAlchemy é uma biblioteca do Python utilizada para trabalhar com bancos de dados relacionais. Ela facilita a comunicação entre uma aplicação Python e o banco de dados.
Seu principal objetivo é permitir que o desenvolvedor possa conectar, consultar, inserir, atualizar e excluir dados de um banco de dados utilizando Python.
O SQLAlchemy também possui recursos que ajudam a evitar a necessidade de escrever todo o SQL manualmente, principalmente através do ORM (Object-Relational Mapping).

2- Que tipo de banco de dados ela permite acessar?
O SQLAlchemy permite trabalhar com diversos bancos de dados relacionais, por exemplo:
MySQL;
PostgreSQL;
SQLite;
Microsoft SQL Server;
Oracle.
Para cada banco de dados, normalmente é utilizado um driver específico que permite a comunicação entre o Python e o banco.
Por exemplo, para SQLite, que já vem integrado ao Python, não é necessário instalar um driver adicional.

3- O SQLAlchemy é principalmente indicado para bancos de dados relacionais.
Ele foi desenvolvido para trabalhar com bancos que utilizam conceitos como:
tabelas; colunas; registros; chaves primárias; relacionamentos entre tabelas; SQL. Portanto, não é uma biblioteca voltada diretamente para bancos não relacionais, como MongoDB ou Redis.

4. A biblioteca trabalha com SQL puro, ORM ou ambos?
O SQLAlchemy trabalha com ambos SQL Puro e ORM. SQL - é possível executar comandos SQL diretamente utilizando a biblioteca.
Exemplo:
from sqlalchemy import create_engine, text
engine = create_engine("sqlite:///banco.db")
with engine.connect() as conexao:
    resultado = conexao.execute(
        text("SELECT * FROM usuarios")
    )
    for linha in resultado:
        print(linha)
Nesse exemplo, o comando SELECT foi escrito diretamente em SQL.

ORM
O SQLAlchemy também possui o ORM, que significa Object-Relational Mapping.
Com o ORM, tabelas do banco podem ser representadas como classes Python. Dessa forma, o programador pode trabalhar com objetos Python em vez de escrever todos os comandos SQL manualmente.
Exemplo simplificado:
from sqlalchemy.orm import DeclarativeBase, Mapped, mapped_column
class Base(DeclarativeBase):
    pass
class Usuario(Base):
    __tablename__ = "usuarios"
    id: Mapped[int] = mapped_column(primary_key=True)
    nome: Mapped[str]

Nesse caso, a tabela usuarios é representada pela classe Usuario.

5. A instalação pode ser feita utilizando o pip, gerenciador de pacotes do Python.
No terminal, basta executar:
pip install SQLAlchemy
Depois da instalação, a biblioteca pode ser importada no código Python:
import sqlalchemy
Para utilizar determinados bancos de dados, também pode ser necessário instalar o driver correspondente.
Por exemplo, para PostgreSQL:
pip install psycopg2-binary

6. Para criar uma conexão, primeiro é necessário criar um engine. O engine é responsável por gerenciar a comunicação entre o programa e o banco de dados.
Um exemplo utilizando SQLite:
from sqlalchemy import create_engine
engine = create_engine("sqlite:///banco.db")
with engine.connect() as conexao:
    print("Conexão realizada com sucesso!")
Nesse exemplo:
create_engine() cria o mecanismo de conexão;
"sqlite:///banco.db" indica que será utilizado um banco SQLite chamado banco.db;
engine.connect() realiza a conexão;
with garante que a conexão seja encerrada corretamente depois do uso.

7. Para executar um SELECT, podemos utilizar a função text() do SQLAlchemy.
Exemplo:
from sqlalchemy import create_engine, text
engine = create_engine("sqlite:///banco.db")
with engine.connect() as conexao:
    resultado = conexao.execute(
        text("SELECT * FROM usuarios")
    )
    for usuario in resultado:
        print(usuario)
O comando:
SELECT * FROM usuarios significa que queremos selecionar todos os dados da tabela usuarios.
Também podemos selecionar apenas algumas colunas:

from sqlalchemy import create_engine, text
engine = create_engine("sqlite:///banco.db")
with engine.connect() as conexao:
    resultado = conexao.execute(
        text("SELECT id, nome FROM usuarios")
    )
    for usuario in resultado:
        print(usuario.id, usuario.nome)

Nesse caso, serão retornados apenas os campos id e nome.

Abaixo está um exemplo simples reunindo a conexão e a consulta SELECT:
from sqlalchemy import create_engine, text
engine = create_engine("sqlite:///banco.db")
with engine.connect() as conexao:
    resultado = conexao.execute(
        text("SELECT id, nome FROM usuarios")
    )
    for usuario in resultado:
        print(f"ID: {usuario.id} - Nome: {usuario.nome}")

Esse código cria uma conexão com o banco banco.db, executa uma consulta na tabela usuarios e mostra o id e o nome de cada usuário encontrado.

8. Vantagens
Flexibilidade e controle: Ao contrário de outros ORMs (como o do Django), o SQLAlchemy permite transitar facilmente entre o mapeamento de objetos (ORM) e consultas SQL puras ou de baixo nível (Core) quando a performance é crucial.
Abstração de banco de dados: Escreva o código uma vez e rode em diferentes sistemas de banco de dados (PostgreSQL, MySQL, SQLite, Oracle, SQL Server) apenas alterando a string de conexão.
Prevenção contra SQL Injection: Ele utiliza automaticamente consultas parametrizadas (bound parameters), limpando os dados de entrada e protegendo a aplicação contra ataques comuns.
Gerenciamento avançado de sessões: O padrão Unit of Work acumula as alterações na memória e só interage com o banco de dados no momento mais eficiente, reduzindo o número de conexões e transações abertas.
Ecossistema maduro: Integra-se perfeitamente com os principais frameworks web do Python (como Flask, FastAPI e Alembic para migrações de banco de dados).

9. Limitações do SQLAlchemy
Curva de aprendizado íngreme: Por ser extremamente poderoso e flexível, sua API é complexa. Iniciantes podem achar a configuração inicial e os conceitos de "Session" difíceis de compreender.
Sobrecarga de performance (Overhead): O mapeamento de linhas de banco de dados para objetos Python consome mais memória e processamento do que usar drivers de banco de dados puros (como psycopg2 ou asyncpg).
Complexidade em queries gigantes: Para relatórios complexos com dezenas de joins, subconsultas e funções de agregação, escrever o código em sintaxe ORM pode ser mais confuso do que escrever o SQL nativo.
Configuração manual: Diferente do Django, que já vem com o ORM configurado e integrado com um sistema de migrações nativo, no SQLAlchemy você precisa configurar a conexão, às sessões e a ferramenta de migração (Alembic) manualmente.

10. Cenários de Uso
Aplicações Enterprise ou Complexas: Projetos onde as regras de negócio mudam constantemente e o banco de dados possui relacionamentos complexos.
APIs com Flask ou FastAPI: Excelente escolha para microserviços e APIs modernas que exigem alta customização e suporte assíncrono (disponível no SQLAlchemy 1.4/2.0).
Sistemas Multi-banco de dados: Projetos que precisam rodar em SQLite para testes locais, mas utilizam PostgreSQL ou SQL Server em produção.
Migração Gradual de Código: Quando você tem um banco de dados legado e precisa mapear apenas algumas tabelas aos poucos sem quebrar o sistema atual.


# sqlite3
1- O objetivo principal do módulo sqlite3 é fornecer uma interface SQL padronizada e compatível com a especificação DB-API 2.0 (definida pela PEP 249) em Python. Ele permite que aplicações criem, conectem, consultem e gerenciem bancos de dados SQLite diretamente no código, sem a necessidade de administrar um servidor de banco de dados independente.

2- Ela permite acessar o SQLite, que é um sistema de gerenciamento de banco de dados (SGBD) embutido (embedded), autocontido (self-contained), de configuração zero (zero-configuration) e sem servidor (serverless). Ele armazena as tabelas e dados diretamente em um único arquivo de disco (ou temporariamente na memória RAM).

3- A biblioteca é indicada para bancos de dados relacionais. O SQLite opera com o modelo relacional baseado em SQL, oferecendo suporte a tabelas, transações com propriedades ACID (Atomicidade, Consistência, Isolamento e Durabilidade), chaves primárias e estrangeiras, subconsultas e junções (JOINs). 

4- A biblioteca sqlite3 trabalha nativamente com SQL puro. A comunicação com o banco de dados é feita enviando instruções SQL diretamente na forma de strings através de métodos como cursor.execute(), executemany() e executescript(). (Observação: ferramentas de ORM de terceiros, como SQLAlchemy, utilizam a biblioteca sqlite3 por baixo dos panos como driver de conexão, mas a biblioteca padrão do Python opera via SQL puro).

5- Não é necessário instalar nada. O módulo sqlite3 já vem integrado (built-in) na biblioteca padrão da linguagem Python. Para começar a usá-lo, basta incluir a instrução import sqlite3 no seu script.

6- A conexão é criada chamando a função sqlite3.connect(), passando o caminho do arquivo do banco de dados (se o arquivo não existir, ele será criado automaticamente) e, em seguida, instanciando um objeto cursor para executar as operações: 
import sqlite3
#1. Estabelece a conexão com o arquivo de banco de dados
conexao = sqlite3.connect("meu_banco.db")
#2. Cria o objeto cursor para enviar comandos SQL
cursor = conexao.cursor()
print("Conexão estabelecida com sucesso!")
#3. Fecha a conexão ao finalizar
conexao.close()

7- Para executar uma consulta SELECT, utiliza-se o método cursor.execute() com a instrução SQL desejada, e os dados podem ser obtidos via métodos como fetchall(), fetchone() ou iterando diretamente sobre o cursor:
import sqlite3
#Conecta ao banco de dados e cria o cursor
conexao = sqlite3.connect("meu_banco.db")
cursor = conexao.cursor()
#Cria a tabela e insere dados de exemplo para o teste
cursor.execute("CREATE TABLE IF NOT EXISTS usuarios (id INTEGER PRIMARY KEY, nome TEXT)")
cursor.execute("INSERT INTO usuarios (nome) VALUES ('Ana'), ('Carlos')")
conexao.commit()
#Executa a consulta SELECT simples
cursor.execute("SELECT id, nome FROM usuarios")
#Forma 1: Recuperando todos os registros com fetchall()
resultados = cursor.fetchall()
for linha in resultados:
    print(f"ID: {linha[0]}, Nome: {linha[1]}")
#Fecha a conexão
conexao.close()

8- Vantagens
Módulo Nativo (Zero Instalação): O sqlite3 já vem integrado na biblioteca padrão do Python, dispensando a instalação de pacotes externos.
Arquitetura Serverless e Zero Configuração: Não exige a instalação, administração ou execução de um processo servidor separado (como ocorre no PostgreSQL ou MySQL) e não utiliza arquivos de configuração.
Autocontido e Leve: Todo o banco de dados (tabelas, índices e dados) é armazenado em um único arquivo em disco ou mantido temporariamente em memória RAM (:memory:).
Suporte Transacional ACID: Oferece suporte completo a transações mantendo a integridade dos dados sob o padrão ACID (Atomicidade, Consistência, Isolamento e Durabilidade).
Portabilidade (Cross-platform): Os arquivos .db ou .sqlite são totalmente portáveis entre diferentes sistemas operacionais (Linux, Windows, macOS, Android, iOS).
Segurança na Aplicação: Segue o padrão DB-API 2.0 do Python (PEP 249), com suporte a placeholders (? ou :nome) para prevenir ataques de SQL Injection.

9- Limitações
Sem Acesso Direto via Rede: Por ser uma biblioteca embutida e não ter um servidor ativo, não oferece suporte nativo para conexões diretas através de redes de computadores.
Ausência de Autenticação e Controle de Usuários: Não possui sistema interno para criação de usuários, senhas ou concessão de permissões específicas (como GRANT / REVOKE); a segurança fica totalmente dependente do controle de acesso do sistema de arquivos do sistema operacional.
Concorrência de Escrita Limitada: Não é adequado para cenários com alta taxa de operações de escrita simultâneas por múltiplos processos, pois o arquivo/banco precisa ser bloqueado durante a gravação.
Restrição de Escala e Replicação: Não foi projetado para volumetrias massivas de dados (acima de 100 GB) nem para cenários que exijam replicação distribuída entre múltiplos servidores.

10- Cenários de Uso
Aplicações Móveis e Desktop: Banco de dados padrão para aplicativos em smartphones (como o WhatsApp) e softwares locais que necessitam de armazenamento interno.
Sistemas Embarcados e IoT: Dispositivos com recursos limitados de hardware que precisam de um SGBD leve e eficiente.
Prototipagem Rápida e Testes: Ideal para construir protótipos de sistemas em Python e executar testes automatizados usando bancos temporários em memória (:memory:) antes de migrar para bancos como PostgreSQL ou MySQL.
Armazenamento de Configurações e Cache Local: Excelente para guardar preferências do usuário, logs locais ou dados em cache da aplicação.
Aplicações Web de Baixo e Médio Tráfego: Indicado para sites e ferramentas internas onde a taxa de consultas (reads) é predominantemente maior do que a de escritas (writes).


