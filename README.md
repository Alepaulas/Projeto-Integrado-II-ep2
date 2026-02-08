# 🗃️ Entregável Parcial 2 – Projeto Físico de Banco de Dados
Plataforma web de doação e reaproveitamento de materiais escolares


Este entregável tem como objetivo transformar o modelo do sistema de doação de materiais escolares em um projeto físico de banco de dados, definindo como as informações serão armazenadas no MySQL.

📌 Diagrama do Banco de Dados

O diagrama abaixo representa as tabelas do sistema e seus relacionamentos.










# 🧩 Estrutura das Tabelas

O banco de dados foi modelado com as seguintes tabelas principais:
- usuario: armazena os dados dos usuários da plataforma, podendo ser do tipo doadores ou beneficiários.
- material: registra os materiais escolares disponíveis para doação.
- doacao: 
- solicitacao: 

# As tabelas foram definidas com:
Chaves primárias (PK) para identificação única dos registros;
Chaves estrangeiras (FK) para manter a integridade entre as tabelas;
Restrições como NOT NULL e UNIQUE para garantir consistência;
Tipos de dados adequados para cada informação (VARCHAR, INT, ENUM, DATETIME).



TABELA DOAÇÃO: 

Atributos	 | Tipo de Dado   |	Chave  	| Índice |       Restrição                    |
---------- |--------------  |---------|--------|------------------------------------|
doacao_id  |      INT	      |   PK	  |   X	   |NOT NULL, AUTO_INCREMENT            |
doador_id  |	    INT       |   FK    |  	X    |NOT NULL, REFERENCES                |
material_id|    	INT	      |   FK	  |   X	   |NOT NULL, UNIQUE, REFERENCES        |
data_disp  |	DATETIME		  |        	|        |NOT NULL, DEFAULT CURRENT_TIMESTAMP |
status	   |ENUM(disponivel,|         |   X    |NOT NULL, DEFAULT                   |
           |reservado,doado)|	 


TABELA SOLICITAÇÃO:

Atributos	      | Tipo de Dado      |	Chave   | Índice |       Restrição                    |
--------------- |-------------------|---------|--------|------------------------------------|
solicitacao_id  |     INT	          |   PK	  |   X	   |NOT NULL, AUTO_INCREMENT            |
doacao_id       |	    INT           |   FK    |   X    |NOT NULL, REFERENCES                |
usuario_id      |    	INT	          |   FK	  |   X	   |NOT NULL, UNIQUE, REFERENCES        |
data_solicitacao|	    TEXT		      |         |        |NULL                                |
mensagem_status	|ENUM(pendente,     |         |   X    |NOT NULL, DEFAULT                   |
                |aprovada,rejeitada)|	 



