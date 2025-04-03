# 📚 Sistema de Gerenciamento de Livraria (Banco de Dados MySQL)

## 📌 Sobre o Projeto
Este projeto consiste em um banco de dados relacional para o gerenciamento de uma livraria, incluindo informações sobre livros, estoque, vendas e vendedores.

## 🏗️ Estrutura do Banco de Dados
O banco de dados é composto pelas seguintes tabelas:

### 📖 LIVROS
Armazena os livros disponíveis na livraria.

```sql
CREATE TABLE LIVROS(
    ID_LIVRO INT NOT NULL,
    NOME_LIVRO VARCHAR(100) NOT NULL,
    AUTORIA VARCHAR(100) NOT NULL,
    EDITORA VARCHAR(100) NOT NULL,
    CATEGORIA VARCHAR(100) NOT NULL,
    PRECO DECIMAL(5,2) NOT NULL,
    PRIMARY KEY (ID_LIVRO)
);
```

### 🏪 ESTOQUE
Registra a quantidade disponível de cada livro.

```sql
ALTER TABLE ESTOQUE ADD CONSTRAINT CE_ESTOQUE_LIVROS
FOREIGN KEY (ID_LIVRO)
REFERENCES LIVROS (ID_LIVRO)
ON DELETE NO ACTION
ON UPDATE NO ACTION;
```

### 🛒 VENDAS
Guarda as informações das vendas realizadas.

```sql
ALTER TABLE VENDAS ADD CONSTRAINT CE_VENDAS_LIVROS
FOREIGN KEY (ID_LIVRO)
REFERENCES LIVROS(ID_LIVRO)
ON DELETE NO ACTION
ON UPDATE NO ACTION;

ALTER TABLE VENDAS ADD CONSTRAINT CE_VENDAS_VENDEDORES
FOREIGN KEY (ID_VENDEDOR)
REFERENCES VENDEDORES (ID_VENDEDOR)
ON DELETE NO ACTION
ON UPDATE NO ACTION;
```

### 👨‍💼 VENDEDORES
Contém os dados dos vendedores da livraria.

```sql
INSERT INTO VENDEDORES VALUES
(1,'Paula Rabelo'),
(2,'Juliana Macedo'),
(3,'Roberto Barros'),
(4,'Barbara Jales');
```

## 🔍 Consultas Úteis
### 1️⃣ Selecionar todos os livros
```sql
SELECT * FROM LIVROS;
```

### 2️⃣ Listar apenas os livros de romance que custam menos de R$48,00
```sql
SELECT * FROM LIVROS
WHERE CATEGORIA = "ROMANCE" AND PRECO < 48;
```

### 3️⃣ Identificar quais livros de poesia **não** são de "Luís Vaz de Camões" ou "Gabriel Pedrosa"
```sql
SELECT * FROM LIVROS
WHERE CATEGORIA = "POESIA" AND NOT(AUTORIA = "Luís Vaz de Camões" OR AUTORIA = "Gabriel Pedrosa");
```

### 4️⃣ Exibir a quantidade de livros vendidos por cada vendedor
```sql
SELECT VENDAS.ID_VENDEDOR, VENDEDORES.NOME_VENDEDOR, SUM(VENDAS.QTD_VENDIDA) AS "Quantidade Vendida"
FROM VENDAS INNER JOIN VENDEDORES
ON VENDAS.ID_VENDEDOR = VENDEDORES.ID_VENDEDOR
GROUP BY VENDAS.ID_VENDEDOR
ORDER BY "Quantidade Vendida";
```

### 5️⃣ Aplicar um desconto de 10% em todos os livros
```sql
UPDATE LIVROS
SET PRECO = 0.9 * PRECO;
```

## 🚀 Como Usar
1. Importe o esquema do banco de dados no MySQL.
2. Execute os scripts de criação de tabelas e inserção de dados.
3. Utilize as consultas SQL fornecidas para interagir com os dados.

---
📌 **Autor:** Vini | 🚀 Desenvolvido para fins de aprendizado e prática com MySQL.

