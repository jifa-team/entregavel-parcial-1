## Entregável Parcial - EP1 🗃️

![drawSQL-image-export-2024-06-09 (2)](https://github.com/jifa-team/entregavel-parcial-1/assets/141689100/356456ac-ad89-4a6e-bfb9-83a85adac199)



> envolve o desenvolvimento do Projeto Físico de Banco de Dados do MVP:

 -  **Requisitos:** Projete as tabelas do banco de dados com base no modelo conceitual, definindo tipos de dados, chaves primárias e estrangeiras, índices, restrições de integridade, etc.
 
 ### 📂 Produzido (*clique no título para abrir documento*): 

👣 [Entedimento da #Sprint 1](https://docs.google.com/document/d/1WD88m6wrEMMfo1sy6NO4tBrnCrWBIqSFBo3LDU8v-ZA/edit?usp=sharing)

Passo inicial que julgamos necessário para entender o que deveríamos realizar para obter êxito ao término da Sprint 1.

👣 [Projeção de tabelas e Dicionario de Dados](https://docs.google.com/document/d/1f60iJDKugPyi7TcIPD92wlHSp3XE5jMtMAvRrACbA7w/edit)

Nesse documento realizamos a descrição das tabelas e seus relacionamentos, assim também como cada um dos seus atributos, além de identificamos quais as tabelas necessitaríamos para o projeto, passo importante para a idealização do projeto físico.

👣 **Modelagem SQL para Prototipar o Desenho do Modelo Físico.**

Nessa parte, fizemos o desenvolvimento dos códigos das tabelas e relacionamentos e atributos na linguagem SQL, para posteriormente podermos gerar o modelo fisico.


    CREATE TABLE clinica (
        clinica_id INT PRIMARY KEY AUTO_INCREMENT,
        cnpj CHAR(14) NOT NULL UNIQUE,
        razao_social VARCHAR(60) NOT NULL,
        nome_fantasia VARCHAR(60) NOT NULL,
        endereco VARCHAR(100) NOT NULL,
        telefone CHAR(11) NOT NULL,
        email VARCHAR(256) NOT NULL,
        registro_conselho INT(10) NOT NULL,
        plano_id INT,
        FOREIGN KEY (plano_id) REFERENCES plano(plano_id)
    );
    
    CREATE TABLE paciente (
        paciente_id INT PRIMARY KEY AUTO_INCREMENT,
        cpf VARCHAR(11) NOT NULL,
        nome_paciente VARCHAR(50) NOT NULL,
        plano_id INT,
        FOREIGN KEY (plano_id) REFERENCES plano(plano_id)
    );
    
    CREATE TABLE dentista (
        dentista_id INT PRIMARY KEY AUTO_INCREMENT,
        numero_cro VARCHAR(10) NOT NULL UNIQUE,
        nome_dentista VARCHAR(50) NOT NULL,
        especializacao VARCHAR(50),
        certificacao VARCHAR(50),
        email VARCHAR(256) NOT NULL UNIQUE,
        telefone CHAR(11) NOT NULL,
        clinica_id INT NOT NULL,
        consultorio_id INT NOT NULL,
        FOREIGN KEY (clinica_id) REFERENCES clinica(clinica_id),
        FOREIGN KEY (consultorio_id) REFERENCES consultorio(consultorio_id)
    );
    
    CREATE TABLE consultorio (
        consultorio_id INT PRIMARY KEY AUTO_INCREMENT,
        nome_consultorio VARCHAR(30) NOT NULL,
        dentista_id INT NOT NULL,
        historico_consultas TEXT NOT NULL,
        telefone CHAR(11) NOT NULL,
        data_funcionamento DATETIME NOT NULL,
        FOREIGN KEY (dentista_id) REFERENCES dentista(dentista_id)
    );
    
    CREATE TABLE plano (
        plano_id INT PRIMARY KEY AUTO_INCREMENT,
        nome_plano VARCHAR(50) NOT NULL,
        descricao VARCHAR(100),
        cobertura TEXT,
        vigencia_inicio DATE NOT NULL,
        vigencia_fim DATE,
        valor_mensal DECIMAL(10, 2) NOT NULL
    );
    
    CREATE TABLE consulta (
        consulta_id INT PRIMARY KEY AUTO_INCREMENT,
        data_consulta DATETIME NOT NULL,
        paciente_id INT NOT NULL,
        dentista_id INT NOT NULL,
        consultorio_id INT NOT NULL,
        valor_consulta DECIMAL(10, 2) NOT NULL,
        descricao_consulta TEXT,
        status_consulta ENUM('Agendada', 'Realizada', 'Cancelada') DEFAULT 'Agendada',
        FOREIGN KEY (paciente_id) REFERENCES paciente(paciente_id),
        FOREIGN KEY (dentista_id) REFERENCES dentista(dentista_id),
        FOREIGN KEY (consultorio_id) REFERENCES consultorio(consultorio_id)
    );



