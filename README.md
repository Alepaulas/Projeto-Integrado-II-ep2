# 🗃️ Entregável Parcial 2 – Projeto Físico de Banco de Dados
Plataforma web de doação e reaproveitamento de materiais escolares


Este entregável tem como objetivo transformar o modelo do sistema de doação de materiais escolares em um projeto físico de banco de dados, definindo como as informações serão armazenadas no MySQL.

📌 Diagrama do Banco de Dados

O diagrama abaixo representa as tabelas do sistema e seus relacionamentos.


<img width="777" height="523" alt="datagrama_mysql_doacao" src="https://github.com/user-attachments/assets/7593e8d1-dede-4f96-b46b-e5c5ad786776" />




# 🧩 Estrutura das Tabelas

O banco de dados foi modelado com as seguintes tabelas principais:
- usuario: armazena os dados dos usuários da plataforma, podendo ser do tipo doadores ou beneficiários.
- material: registra os materiais escolares disponíveis para doação.
- doacao: representa o material que será doado com status e data de disponibilização.
- solicitacao: armazena as solicitações feitas pelos usuários com data de solicitação e status do pedido.

# As tabelas foram definidas com:
Chaves primárias (PK) para identificação única dos registros;
Chaves estrangeiras (FK) para manter a integridade entre as tabelas;
Restrições como NOT NULL e UNIQUE para garantir consistência;
Tipos de dados adequados para cada informação (VARCHAR, INT, ENUM, DATETIME).

TABELA USUÁRIO:

| Atributos  | Tipo de Dado               | Chave | Índice | Restrição                           |
| ---------- | -------------------------- | ----- | ------ | ----------------------------------- |
| usuario_id | INT                        | PK    | X      | NOT NULL, AUTO_INCREMENT            |
| nome       | VARCHAR(85)                |       |        | NOT NULL                            |
| email      | VARCHAR(120)               |       | X      | NOT NULL, UNIQUE                    |
| senha      | VARCHAR(255)               |       |        | NOT NULL                            |
| tipo       | ENUM(beneficiario, doador) |       | X      | NOT NULL                            |
| criado_em  | DATETIME                   |       |        | NOT NULL, DEFAULT CURRENT_TIMESTAMP |


TABELA MATERIAL:

| Atributos          | Tipo de Dado      | Chave | Índice | Restrição                |
| ------------------ | ----------------- | ----- | ------ | ------------------------ |
| material_id        | INT               | PK    | X      | NOT NULL, AUTO_INCREMENT |
| nome               | VARCHAR(85)       |       | X      | NOT NULL                 |
| categoria          | VARCHAR(50)       |       | X      | NOT NULL                 |
| descricao          | TEXT              |       |        | NOT NULL                 |
| estado_conservacao | ENUM(novo, usado) |       |        | NOT NULL                 |


TABELA DOAÇÃO: 

Atributos	 | Tipo de Dado   |	Chave  	| Índice |       Restrição                    |
---------- |--------------  |---------|--------|------------------------------------|
doacao_id  |      INT	      |   PK	  |   X	   |NOT NULL, AUTO_INCREMENT            |
doador_id  |	    INT       |   FK    |  	X    |NOT NULL, REFERENCES                |
material_id|    	INT	      |   FK	  |   X	   |NOT NULL, UNIQUE, REFERENCES        |
data_disp  |	DATETIME		  |        	|        |NOT NULL, DEFAULT CURRENT_TIMESTAMP |
status	   |ENUM(disponivel,reservado, doado|         |   X    |NOT NULL, DEFAULT                   |


TABELA SOLICITAÇÃO:

Atributos	      | Tipo de Dado      |	Chave   | Índice |       Restrição                    |
--------------- |-------------------|---------|--------|------------------------------------|
solicitacao_id  |     INT	          |   PK	  |   X	   |NOT NULL, AUTO_INCREMENT            |
doacao_id       |	    INT           |   FK    |   X    |NOT NULL, REFERENCES                |
usuario_id      |    	INT	          |   FK	  |   X	   |NOT NULL, REFERENCES        |
data_solicitacao|	    TEXT		      |         |        |NULL                                |
mensagem_status	|ENUM(pendente, aprovada, rejeitada)     |         |   X    |NOT NULL, DEFAULT                   |



