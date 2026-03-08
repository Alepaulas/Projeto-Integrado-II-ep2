# 🗃️ Entregável Parcial 2 – Projeto Físico de Banco de Dados
Plataforma web de doação e reaproveitamento de materiais escolares


Este entregável tem como objetivo transformar o modelo do sistema de doação de materiais escolares em um projeto físico de banco de dados, definindo como as informações serão armazenadas no MySQL.

📌 Diagrama do Banco de Dados

O diagrama abaixo representa as tabelas do sistema e seus relacionamentos.


<img width="777" height="523" alt="datagrama_mysql_doacao" src="https://github.com/user-attachments/assets/7593e8d1-dede-4f96-b46b-e5c5ad786776" />



## 📝[Relatório da Atividade](https://docs.google.com/document/d/1emMiAg7GH-lP7LxfwCPgrTagoQ2P7Xg9CYx2CFunj_4/edit?tab=t.0)


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
| Atributos            | Tipo de Dado                   | Chave | Índice | Restrição                           |
| -------------------- | ------------------------------ | ----- | ------ | ----------------------------------- |
| usuario_id           | INT                            | PK    | X      | NOT NULL, AUTO_INCREMENT            |
| nome                 | VARCHAR(85)                    |       |        | NOT NULL                            |
| cpf                  | VARCHAR(11)                    |       | X      | NOT NULL, UNIQUE                    |
| rg                   | VARCHAR(20)                    |       |        | NULL                                |
| data_nascimento      | DATE                           |       |        | NOT NULL                            |
| situacao_educacional | ENUM(estudante, nao_estudante) |       |        | NOT NULL                            |
| logradouro           | VARCHAR(120)                   |       |        | NOT NULL                            |
| bairro               | VARCHAR(80)                    |       |        | NOT NULL                            |
| cidade               | VARCHAR(80)                    |       |        | NOT NULL                            |
| uf                   | CHAR(2)                        |       |        | NOT NULL                            |
| email                | VARCHAR(120)                   |       | X      | NOT NULL, UNIQUE                    |
| senha                | VARCHAR(255)                   |       |        | NOT NULL                            |
| tipo                 | ENUM(beneficiario, doador)     |       | X      | NOT NULL                            |
| criado_em            | DATETIME                       |       |        | NOT NULL, DEFAULT CURRENT_TIMESTAMP |


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


# Modelagem SQL para Prototipar o Modelo Físico

Foi desenvolvido o script SQL responsável pela criação das tabelas, seus atributos e relacionamentos, permitindo posteriormente a geração do modelo físico do banco de dados do sistema de doações.

```sql
CREATE TABLE usuario (
  usuario_id INT AUTO_INCREMENT PRIMARY KEY,
  nome VARCHAR(85) NOT NULL,
  cpf VARCHAR(11),
  rg VARCHAR(20),
  data_nascimento DATE,
  situacao_educacional VARCHAR(50),
  logradouro VARCHAR(120),
  bairro VARCHAR(80),
  cidade VARCHAR(80),
  uf CHAR(2),
  email VARCHAR(120) NOT NULL UNIQUE,
  senha VARCHAR(255) NOT NULL,
  tipo ENUM('beneficiario','doador') NOT NULL,
  criado_em DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE material (
  material_id INT AUTO_INCREMENT PRIMARY KEY,
  nome VARCHAR(85) NOT NULL,
  categoria VARCHAR(50) NOT NULL,
  descricao TEXT NOT NULL,
  estado_conservacao ENUM('novo','usado') NOT NULL
);

CREATE TABLE doacao (
  doacao_id INT AUTO_INCREMENT PRIMARY KEY,
  doador_id INT NOT NULL,
  material_id INT NOT NULL UNIQUE,
  data_disp DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  status ENUM('disponivel','reservado','doado') NOT NULL DEFAULT 'disponivel',
  FOREIGN KEY (doador_id) REFERENCES usuario(usuario_id),
  FOREIGN KEY (material_id) REFERENCES material(material_id)
);

CREATE TABLE solicitacao (
  solicitacao_id INT AUTO_INCREMENT PRIMARY KEY,
  doacao_id INT NOT NULL,
  usuario_id INT NOT NULL,
  data_solicitacao DATETIME NULL,
  mensagem_status ENUM('pendente','aprovada','rejeitada') NOT NULL DEFAULT 'pendente',
  FOREIGN KEY (doacao_id) REFERENCES doacao(doacao_id),
  FOREIGN KEY (usuario_id) REFERENCES usuario(usuario_id)
);

