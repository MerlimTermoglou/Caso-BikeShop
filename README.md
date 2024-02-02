# Empresa: BikeShop
### Visão Geral:

A BikeShop é uma empresa especializada na venda de bicicletas e acessórios relacionados. 
Localizada em uma área urbana movimentada de Uberlândia, Minas Gerais, a empresa tem 
como objetivo oferecer uma variedade de bicicletas de alta qualidade para ciclistas de todos os 
níveis, desde iniciantes até ciclistas experientes e entusiastas.

### Desafio:

A BikeShop está crescendo rapidamente e enfrenta desafios no gerenciamento eficiente de seu 
inventário, clientes e vendas. Atualmente, eles estão registrando essas informações 
manualmente ou usando planilhas eletrônicas, o que se tornou ineficiente e propenso a erros. 
Eles reconhecem a necessidade de um sistema de banco de dados centralizado que possa 
armazenar e gerenciar essas informações de forma mais eficaz.

### Objetivos do Sistema de Banco de Dados:

Gerenciar o inventário de bicicletas e acessórios, incluindo detalhes como modelo, marca, 
quantidade em estoque, preço de venda e fornecedor.


Manter um registro centralizado de clientes, incluindo informações como nome, endereço, 
número de telefone, endereço de e-mail e histórico de compras.


Registrar e acompanhar as vendas de bicicletas e acessórios, incluindo detalhes como data da 
venda, produtos vendidos, preço de venda, método de pagamento e vendedor responsável.

### Requisitos Funcionais do Sistema de Banco de Dados:

Capacidade de adicionar, atualizar e excluir itens do inventário, bem como verificar a 
disponibilidade de produtos em tempo real.


Capacidade de adicionar novos clientes, atualizar informações existentes e manter um histórico 
de suas compras anteriores.


Funcionalidade para registrar novas vendas, incluindo a associação dos produtos vendidos aos 
clientes correspondentes e a geração de recibos.


Recursos de segurança para proteger os dados do cliente e do inventário contra acesso não 
autorizado.


Capacidade de gerar relatórios de vendas, análises de estoque e dados do cliente para ajudar 
na tomada de decisões comerciais.

### Abordagem Proposta:

A BikeShop planeja desenvolver um sistema de banco de dados personalizado usando 
tecnologias modernas de banco de dados, como MySQL ou PostgreSQL. Eles planejam 
colaborar com desenvolvedores de software especializados para projetar e implementar o 
sistema de acordo com seus requisitos específicos. O sistema será acessado por funcionários 
autorizados por meio de uma interface de usuário intuitiva, onde poderão realizar todas as 
operações necessárias de forma eficiente.

### Benefícios Esperados:

Melhoria na eficiência operacional, permitindo que a BikeShop gerencie seu inventário, clientes 
e vendas de forma mais rápida e precisa.


Maior satisfação do cliente, oferecendo um serviço mais personalizado e mantendo um 
histórico detalhado das interações anteriores.


Melhoria na tomada de decisões comerciais com base em relatórios e análises de dados 
precisos e atualizados.


Com um sistema de banco de dados eficiente e bem projetado, a BikeShop está confiante de 
que poderá atender às demandas de seus clientes de maneira mais eficaz e continuar 
prosperando no mercado de bicicletas.

## Modelo lógico para o estudo de caso
### Tabelas:

### Inventário:

ID_Inventario (Chave Primária)

Modelo

Marca

Quantidade

Preço

ID_Fornecedor (Chave Estrangeira referenciando a tabela de Fornecedores)


### Clientes:
ID_Cliente (Chave Primária)

Nome

Endereço

Número_de_Telefone

Email


### Vendas:
ID_Venda (Chave Primária)

Data

ID_Cliente (Chave Estrangeira referenciando a tabela de Clientes)

ID_Inventario (Chave Estrangeira referenciando a tabela de Inventário)

Quantidade_Vendida

Preço_Total

Método_de_Pagamento

ID_Vendedor (Chave Estrangeira referenciando a tabela de Vendedores)


### Fornecedores:
ID_Fornecedor (Chave Primária)

Nome_do_Fornecedor

Endereço_do_Fornecedor

Número_de_Telefone_do_Fornecedor

Email_do_Fornecedor

### Vendedores:
ID_Vendedor (Chave Primária)

Nome_do_Vendedor

ID_Funcionario (Chave Estrangeira referenciando a tabela de Funcionários)

### Funcionários:
ID_Funcionario (Chave Primária)

Nome_do_Funcionario

Cargo

Salário

Data_de_Admissão

### Relacionamentos:
Um fornecedor pode fornecer múltiplos itens de inventário, mas cada item de inventário é 
fornecido por apenas um fornecedor. (Relacionamento um para muitos entre Fornecedores e 
Inventário)

Um cliente pode fazer várias compras, mas cada compra é feita por apenas um cliente. 
(Relacionamento um para muitos entre Clientes e Vendas)

Cada venda inclui vários itens de inventário, e cada item de inventário pode estar presente em 
várias vendas. (Relacionamento muitos para muitos entre Vendas e Inventário)

Um vendedor pode fazer várias vendas, mas cada venda é realizada por apenas um vendedor. 
(Relacionamento um para muitos entre Vendedores e Vendas)

Cada vendedor é associado a apenas um funcionário. (Relacionamento um para um entre 
Funcionários e Vendedores)

Este modelo lógico de banco de dados reflete as entidades principais e seus relacionamentos 
no contexto da BikeShop, permitindo a organização eficiente dos dados e a realização de 
operações de negócios necessárias.


#

### Com base no estudo de caso acima, foi construido um modelo conceitual para desenvolvimentode um banco de dados que atenda a BikeShop


## Modelo conceitual
!["modelo conceitual do banco de dados"](bikeshop-modeloconceitual.png)

## Modelo Lógico
!["modelo lógico do banco de dados"](bikeshop-modelolgico.png)

## Código SQL para o modelo físico do banco de dados
```sql
-- MySQL Workbench Forward Engineering

SET @OLD_UNIQUE_CHECKS=@@UNIQUE_CHECKS, UNIQUE_CHECKS=0;
SET @OLD_FOREIGN_KEY_CHECKS=@@FOREIGN_KEY_CHECKS, FOREIGN_KEY_CHECKS=0;
SET @OLD_SQL_MODE=@@SQL_MODE, SQL_MODE='ONLY_FULL_GROUP_BY,STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION';

-- -----------------------------------------------------
-- Schema mydb
-- -----------------------------------------------------

-- -----------------------------------------------------
-- Schema mydb
-- -----------------------------------------------------
CREATE SCHEMA IF NOT EXISTS `mydb` DEFAULT CHARACTER SET utf8 ;
USE `mydb` ;

-- -----------------------------------------------------
-- Table `mydb`.`Funcionários`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`Funcionários` (
  `id_funcionario` INT NOT NULL AUTO_INCREMENT,
  `nome_funcionario` VARCHAR(50) NOT NULL,
  `cargo` VARCHAR(15) NOT NULL,
  `salário` DECIMAL(10,5) NOT NULL,
  `data_admissao` DATE NOT NULL,
  PRIMARY KEY (`id_funcionario`))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `mydb`.`Vendedores`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`Vendedores` (
  `id_vendedor` INT NOT NULL AUTO_INCREMENT,
  `nome_vendedor` VARCHAR(45) NOT NULL,
  `id_funcionario` VARCHAR(45) NOT NULL,
  `id_funcionario` INT NOT NULL,
  PRIMARY KEY (`id_vendedor`, `id_funcionario`),
  INDEX `fk_Vendedores_Funcionários1_idx` (`id_funcionario` ASC) VISIBLE,
  CONSTRAINT `fk_Vendedores_Funcionários1`
    FOREIGN KEY (`id_funcionario`)
    REFERENCES `mydb`.`Funcionários` (`id_funcionario`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `mydb`.`Clientes`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`Clientes` (
  `id_clientes` INT NOT NULL AUTO_INCREMENT,
  `nome_cliente` VARCHAR(50) NOT NULL,
  `endereço_cliente` VARCHAR(45) NOT NULL,
  `num_de_telefone_cliente` INT NOT NULL,
  `email_cliente` VARCHAR(30) NOT NULL,
  PRIMARY KEY (`id_clientes`),
  UNIQUE INDEX `email_cliente_UNIQUE` (`email_cliente` ASC) VISIBLE)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `mydb`.`Vendas`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`Vendas` (
  `id_vendas` INT NOT NULL AUTO_INCREMENT,
  `id_clientes` INT NOT NULL,
  `id_inventario` INT NOT NULL,
  `data` DATE NOT NULL,
  `quantidade_vendida` INT NOT NULL,
  `preco_total` DECIMAL(10,5) NOT NULL,
  `metodo_de_pagamento` VARCHAR(15) NOT NULL,
  `id_vendedor` INT NOT NULL,
  `id_vendedor` INT NOT NULL,
  `id_funcionario` INT NOT NULL,
  `id_clientes` INT NOT NULL,
  PRIMARY KEY (`id_vendas`, `id_vendedor`, `id_funcionario`, `id_clientes`),
  INDEX `fk_Vendas_Vendedores1_idx` (`id_vendedor` ASC, `id_funcionario` ASC) VISIBLE,
  INDEX `fk_Vendas_Clientes1_idx` (`id_clientes` ASC) VISIBLE,
  CONSTRAINT `fk_Vendas_Vendedores1`
    FOREIGN KEY (`id_vendedor` , `id_funcionario`)
    REFERENCES `mydb`.`Vendedores` (`id_vendedor` , `id_funcionario`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION,
  CONSTRAINT `fk_Vendas_Clientes1`
    FOREIGN KEY (`id_clientes`)
    REFERENCES `mydb`.`Clientes` (`id_clientes`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `mydb`.`Inventário`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`Inventário` (
  `id_inventario` INT NOT NULL AUTO_INCREMENT,
  `modelo` VARCHAR(30) NOT NULL,
  `marca` VARCHAR(30) NOT NULL,
  `quantidade` INT NOT NULL,
  `preco` DECIMAL(10,5) NOT NULL,
  `id_fornecedor` INT NOT NULL,
  `id_vendas` INT NOT NULL,
  PRIMARY KEY (`id_inventario`, `id_vendas`),
  INDEX `fk_Inventáio_Vendas1_idx` (`id_vendas` ASC) VISIBLE,
  CONSTRAINT `fk_Inventáio_Vendas1`
    FOREIGN KEY (`id_vendas`)
    REFERENCES `mydb`.`Vendas` (`id_vendas`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `mydb`.`Fornecedores`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`Fornecedores` (
  `id_fornecedores` INT NOT NULL AUTO_INCREMENT,
  `nome_fornecedor` VARCHAR(50) NOT NULL,
  `endereço_fornecedor` VARCHAR(50) NOT NULL,
  `num_telefone_fornecedor` INT NOT NULL,
  `email_fornecedor` VARCHAR(50) NOT NULL,
  `id_inventario` INT NOT NULL,
  `id_vendas` INT NOT NULL,
  PRIMARY KEY (`id_fornecedores`, `id_inventario`, `id_vendas`),
  UNIQUE INDEX `email_fornecedor_UNIQUE` (`email_fornecedor` ASC) VISIBLE,
  INDEX `fk_Fornecedores_Inventáio1_idx` (`id_inventario` ASC, `id_vendas` ASC) VISIBLE,
  CONSTRAINT `fk_Fornecedores_Inventáio1`
    FOREIGN KEY (`id_inventario` , `id_vendas`)
    REFERENCES `mydb`.`Inventário` (`id_inventario` , `id_vendas`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


SET SQL_MODE=@OLD_SQL_MODE;
SET FOREIGN_KEY_CHECKS=@OLD_FOREIGN_KEY_CHECKS;
SET UNIQUE_CHECKS=@OLD_UNIQUE_CHECKS;

```