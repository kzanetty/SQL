## SQL
Salvar comandos SQL


# Aula 1

```SQL 
CREATE TABLE IF NOT EXISTS usuario (
  idUsuario INT NOT NULL PRIMARY KEY,
  cpf INT NOT NULL UNIQUE,
  nome VARCHAR(255) NULL,
  dataAniversario TIMESTAMP NOT NULL
);

CREATE TABLE conta (
	idConta INT NOT NULL GENERATED ALWAYS AS IDENTITY,
	dataCriacao TIMESTAMP NOT NULL,
	valorLimite NUMERIC(5,2) NOT NULL CHECK( valorLimite >0),
	idUsuario INT NOT NULL,
	PRIMARY KEY (idConta),
	FOREIGN KEY (idUsuario) REFERENCES usuario (idUsuario)
);

INSERT INTO usuario VALUES (1, 00000000023, 'Henrique', '2022-07-01');

INSERT INTO usuario VALUES (2, 00000000023, 'Henrique', '2022-07-01');

INSERT INTO conta(dataCriacao, valorLimite, idUsuario) VALUES ('2022-10-03', 530.23, 1);

ALTER TABLE usuario ADD COLUMN telefone VARCHAR(11) NOT NULL DEFAULT '00-00000000';

ALTER TABLE usuario DROP COLUMN dataAniversario;

ALTER TABLE usuario RENAME telefone TO contato;

ALTER TABLE usuario ALTER COLUMN contato DROP NOT NULL;

ALTER TABLE usuario ALTER COLUMN contato SET NOT NULL;

ALTER TABLE usuario ALTER COLUMN nome SET DEFAULT 'Não informado';

ALTER TABLE usuario ADD CONSTRAINT cpf_usuario_check CHECK(cpf > 0);

DROP TABLE IF EXISTS conta;

DROP TABLE usuario CASCADE;
```


### GENERATED ALWAYS AS IDENTITY
-Significa que a chave primaria para essa tabela ira ser gerada de forma automática. "AS IDENTITY" não permite que seja passado uma PK na inserção de um objeto no DB e irá resultar em um erro.

### GENERATED ALWAYS BY DEFAULT
-Significa que a chave primaria para essa tabela ira ser gerada de forma automática, mas caso seja informada uma primary key na inserção desse objeto no banco de dados, ele ira aceitar.

### 	PRIMARY KEY (idConta), FOREIGN KEY (idUsuario) REFERENCES usuario (idUsuario)
- PRIMARY KEY (idConta) -> Informa que a PK dessa tabela sera a coluna idConta.
- FOREIGN KEY (idUsuario) REFERENCES usuario (idUsuario) -> Informa que a chave estrangeira sera a coluna idUsuario, e que tem referência na tabela 'usuario', com a pk da coluna 'idConta'.


### Textos, chars e datas
- Devem ser informados entre ' '.

### ALTER TABLE usuario ADD COLUMN telefone VARCHAR(11) NOT NULL DEFAULT '00-00000000'
- Ira adicionar uma nova coluna na tabela já existente 'usuario'. Ela sera do tipo VARCHAR e tera um maximo de 11 caracteres. Por padrão, todos os campos de telefone que não forem informados, serão preenchidos com '00-00000000'.

### ALTER TABLE usuario DROP COLUMN dataAniversario;
- Esse comando ira excluir a coluna dataAniversario da tabela usuário.

### ALTER TABLE usuario RENAME telefone TO contato
- Ira alterar, na tabela usuário, o nome da coluna telefone para contato.

### ALTER TABLE usuario ALTER COLUMN contato DROP NOT NULL
Isso ira excluir a restrição 'NOT NULL'. Ou seja, agora  a coluna contato ira aceitar valor nulo.


### ALTER TABLE usuario ALTER COLUMN contato SET NOT NULL
- Com esse comando nos informarmos que a coluna 'contato' agora não aceita mais valores nulos.

### ALTER TABLE usuario ALTER COLUMN nome SET DEFAULT 'Não informado'
- Isso ira adicionar um valor default na coluna nome. Caso não seja informado um nome na inserção do objeto no BD, o valor padrão sera 'Não informado'.

### ALTER TABLE usuario ADD CONSTRAINT cpf_usuario_check CHECK(cpf > 0)
- Isso iria adicionar uma restrição na coluna cpf. Obrigatoriamente o cpf deve ser maios que 0.

### DROP TABLE IF EXISTS conta
- Ira excluir a table conta, caso ela exista.

### DROP TABLE usuario CASCADE
- Ira excluir a tabela usuário. Supondo que ela tenha dependência com outras tabelas, caso seja feito a tentativa de exclusão sem o 'CASCADE', não sera possível excluir.
