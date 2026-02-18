
# Projeto de Banco de Dados – Oficina Mecânica

##  Descrição do Projeto

Este projeto apresenta o **modelo conceitual de banco de dados** para um sistema de **controle e gerenciamento de ordens de serviço em uma oficina mecânica**, desenvolvido com base na narrativa proposta no desafio da DIO.

O objetivo do sistema é permitir o cadastro de clientes, veículos, mecânicos, serviços e peças, além do controle completo das **Ordens de Serviço (OS)**, desde a abertura até a conclusão dos trabalhos.

O modelo foi elaborado seguindo boas práticas de **modelagem conceitual**, **normalização** e **relacionamentos adequados**, garantindo consistência, flexibilidade e aderência às regras de negócio descritas.

---

##  Objetivo do Sistema

- Controlar a execução de ordens de serviço em uma oficina mecânica  
- Registrar clientes e seus veículos  
- Associar veículos a ordens de serviço  
- Registrar os serviços realizados e as peças utilizadas  
- Associar equipes de mecânicos às ordens de serviço  
- Calcular o valor total da OS com base em mão de obra e peças  

---

##  Entidades do Modelo

###  Cliente
Representa o cliente da oficina.

**Atributos:**
- idCliente
- nome
- cpf

**Relacionamento:**
- Um cliente pode possuir **um ou vários veículos**

---

###  Veículo
Representa os veículos levados à oficina.

**Atributos:**
- idVeiculo
- placa
- modelo
- ano
- fk_idCliente

**Relacionamento:**
- Cada veículo pertence a **um cliente**
- Um veículo pode ter **várias ordens de serviço**

---

###  Ordem_de_serviço (OS)
Representa a ordem de serviço emitida para um veículo.

**Atributos:**
- idOS
- data_emissão
- valor
- status
- data_conclusão
- fk_idVeiculo

**Observação:**
O valor da OS é composto pela soma dos valores dos serviços (mão de obra) e das peças utilizadas.

---

###  Mecânico
Representa os mecânicos da oficina.

**Atributos:**
- idMecanico
- nome
- endereco
- especialidade

**Relacionamento:**
- Um mecânico pode participar de **várias ordens de serviço**
- Uma ordem de serviço pode ter **vários mecânicos**

Esse relacionamento N:N é resolvido pela tabela associativa **OS_Mecanico**.

---

###  Serviço
Representa os serviços executados na oficina (ex: revisão, troca de óleo, conserto).

**Atributos:**
- idServico
- descricao
- valorMaoDeObra

**Relacionamento:**
- Um serviço pode estar em **várias ordens de serviço**
- Uma ordem de serviço pode conter **vários serviços**

Relacionamento resolvido pela tabela **OS_Servico**.

---

###  Peça
Representa as peças utilizadas nos serviços.

**Atributos:**
- idPeca
- nome
- valor

**Relacionamento:**
- Uma peça pode ser utilizada em **várias ordens de serviço**
- Uma ordem de serviço pode utilizar **várias peças**

Relacionamento resolvido pela tabela **OS_Peca**.

---

##  Tabelas Associativas

### OS_Mecanico
Relaciona mecânicos às ordens de serviço.

- fk_idMecanico
- fk_idOS  
**Chave primária composta:** (fk_idMecanico, fk_idOS)

---

### OS_Servico
Relaciona serviços às ordens de serviço.

- fk_idOS
- fk_idServico  
**Chave primária composta:** (fk_idOS, fk_idServico)

---

### OS_Peca
Relaciona peças às ordens de serviço.

- fk_idOS
- fk_idPeca  
**Chave primária composta:** (fk_idOS, fk_idPeca)

---

##  Decisões de Modelagem

- Relacionamentos **N:N** foram resolvidos com tabelas associativas
- A entidade **Veículo** foi criada para refletir corretamente a narrativa
- Serviços e peças não são atributos da OS, mas entidades independentes
- O valor da OS pode ser calculado dinamicamente ou armazenado para fins históricos
- O modelo está normalizado, evitando redundâncias e inconsistências

---

## 📷 Diagrama

O diagrama conceitual completo está disponível nos arquivos:
- `ecommerce.pdf`
- `ecommerce.png`
