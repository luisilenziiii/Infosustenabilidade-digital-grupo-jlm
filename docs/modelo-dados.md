# Modelo de Dados – Banco de Dados de Coleta e Descarte de Resíduos

## Visão Geral

Este banco de dados foi estruturado para armazenar informações relacionadas a pontos de coleta de resíduos, materiais aceitos, procedimentos de descarte, evidências de pesquisa e análises críticas sobre a infraestrutura de descarte em diferentes municípios.

A estrutura permite centralizar informações sobre locais de coleta, seus serviços e avaliações sobre acessibilidade e divulgação.

---

# Modelo Conceitual

O sistema possui cinco entidades principais:

- `pontos_coleta`
- `materiais_aceitos`
- `procedimentos_descarte`
- `evidencia`
- `analise_critica`

Relacionamento principal:

```text
pontos_coleta
     |
     |---< materiais_aceitos
     |
     |---< procedimentos_descarte
     |
     |---< evidencia

analise_critica
(independente)
```

---

# Estrutura das Tabelas

## 1. pontos_coleta

Tabela principal contendo informações dos locais de descarte.

| Campo | Tipo | Descrição |
|---|---:|---|
| ID | Inteiro | Identificador do ponto de coleta |
| NOME | Texto | Nome do ponto de coleta |
| ENDEREÇO | Texto | Endereço completo |
| BAIRRO | Texto | Bairro |
| CIDADE | Texto | Município |
| CONTATO | Texto | Telefone ou forma de contato |
| LINK_MAPS | Texto | Link para localização |

### Exemplo

| ID | NOME | CIDADE |
|---|---|---|
| 1 | (PEV)/SAMAE | Blumenau |

---

## 2. materiais_aceitos

Armazena os tipos de materiais recebidos em cada ponto.

| Campo | Tipo | Descrição |
|---|---:|---|
| ID_MATERIAL | Inteiro | Identificador do registro |
| ID_PONTO | Inteiro | Chave estrangeira para ponto de coleta |
| TIPO_MATERIAL_ACEITO | Texto | Materiais recebidos |
| OBSERVAÇÃO | Texto | Observações adicionais |

### Relacionamento

```text
ID_PONTO → pontos_coleta.ID
```

### Cardinalidade

Um ponto de coleta pode aceitar vários materiais:

```text
1 ponto_coleta ---- N materiais_aceitos
```

---

## 3. procedimentos_descarte

Armazena regras e orientações de descarte.

| Campo | Tipo | Descrição |
|---|---:|---|
| ID | Inteiro | Identificador |
| ID_PONTO | Inteiro | Referência ao ponto |
| HORÁRIOS | Texto | Horário de funcionamento |
| AGENDAMENTO | Texto | Necessidade de agendamento |
| CUSTO | Texto | Informação sobre cobrança |
| MODALIDADE | Texto | Forma de descarte |

### Relacionamento

```text
ID_PONTO → pontos_coleta.ID
```

### Cardinalidade

```text
1 ponto_coleta ---- N procedimentos_descarte
```

---

## 4. evidencia

Registra evidências e fontes utilizadas na pesquisa.

| Campo | Tipo | Descrição |
|---|---:|---|
| ID | Inteiro | Identificador |
| ID_PONTO | Inteiro | Referência ao ponto |
| TIPO | Texto | Tipo de evidência |
| DESCRIÇÃO | Texto | Detalhes da evidência |
| ARQUIVO/LINK | Texto | Link ou arquivo relacionado |
| DATA | Data | Data do registro |

### Relacionamento

```text
ID_PONTO → pontos_coleta.ID
```

### Cardinalidade

```text
1 ponto_coleta ---- N evidencias
```

---

## 5. analise_critica

Tabela destinada à avaliação qualitativa dos municípios.

Essa entidade funciona de forma independente das demais tabelas.

| Campo | Tipo | Descrição |
|---|---:|---|
| ID | Inteiro | Identificador |
| CIDADE | Texto | Município analisado |
| FACILIDADE | Texto | Pontos positivos encontrados |
| DIFICULDADE | Texto | Problemas observados |
| DIVULGAÇÃO | Texto | Situação da divulgação |
| MELHORIAS | Texto | Sugestões futuras |

---

# Modelo Relacional

```text
PONTOS_COLETA
-------------
ID (PK)
NOME
ENDEREÇO
BAIRRO
CIDADE
CONTATO
LINK_MAPS


MATERIAIS_ACEITOS
-----------------
ID_MATERIAL (PK)
ID_PONTO (FK)
TIPO_MATERIAL_ACEITO
OBSERVAÇÃO


PROCEDIMENTOS_DESCARTE
----------------------
ID (PK)
ID_PONTO (FK)
HORÁRIOS
AGENDAMENTO
CUSTO
MODALIDADE


EVIDENCIA
----------
ID (PK)
ID_PONTO (FK)
TIPO
DESCRIÇÃO
ARQUIVO/LINK
DATA


ANALISE_CRITICA
---------------
ID (PK)
CIDADE
FACILIDADE
DIFICULDADE
DIVULGAÇÃO
MELHORIAS
```

---

# Regras de Negócio

- Cada ponto de coleta pode aceitar vários materiais.
- Cada ponto de coleta pode possuir múltiplos procedimentos.
- Cada ponto pode possuir diversas evidências associadas.
- Análises críticas são independentes e representam avaliações por município.
- O sistema concentra informações sobre descarte de resíduos eletrônicos e reciclagem.

---

# Possíveis Melhorias Futuras

Sugestões para normalização e evolução do banco:

- Criar tabela `cidade`
- Criar tabela `bairro`
- Separar materiais em tabela própria
- Padronizar horários
- Criar categoria de resíduos
- Utilizar URLs validadas
- Inserir geolocalização (latitude/longitude)
- Implementar status ativo/inativo dos pontos

---

# Tecnologias Indicadas

Banco compatível com:

- MySQL
- PostgreSQL
- SQL Server
- SQLite

