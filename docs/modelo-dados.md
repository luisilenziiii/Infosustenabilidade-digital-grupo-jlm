<div align="center">

# 📊 Modelo de Dados – Banco de Dados de Coleta e Descarte de Resíduos

### ♻️ Estrutura de dados para gerenciamento de pontos de coleta e descarte

![Status](https://img.shields.io/badge/Status-Em%20Desenvolvimento-green)
![Banco](https://img.shields.io/badge/Banco-Relacional-blue)
![Modelo](https://img.shields.io/badge/Modelo-Conceitual-orange)
![Licença](https://img.shields.io/badge/Licença-MIT-purple)

</div>

---

## 🌎 Visão Geral

Este banco de dados foi estruturado para armazenar informações relacionadas a **pontos de coleta de resíduos**, materiais aceitos, procedimentos de descarte, evidências de pesquisa e análises críticas.

O objetivo é centralizar informações sobre locais de coleta, serviços disponíveis e avaliações sobre acessibilidade e divulgação.

---

# 🧩 Modelo Conceitual

O sistema possui cinco entidades principais:

📍 `pontos_coleta`  
♻️ `materiais_aceitos`  
📋 `procedimentos_descarte`  
📎 `evidencia`  
📈 `analise_critica`

### Relacionamentos

```text
📍 pontos_coleta
        |
        |---< ♻️ materiais_aceitos
        |
        |---< 📋 procedimentos_descarte
        |
        |---< 📎 evidencia

📈 analise_critica
(independente)
```

---

# 🗂️ Estrutura das Tabelas

## 📍 1. pontos_coleta

Tabela principal contendo informações dos locais de descarte.

| Campo | Tipo | Descrição |
|:---|:---:|:---|
| 🆔 ID | Inteiro | Identificador do ponto |
| 🏢 NOME | Texto | Nome do local |
| 📍 ENDEREÇO | Texto | Endereço completo |
| 🏘️ BAIRRO | Texto | Bairro |
| 🌆 CIDADE | Texto | Município |
| 📞 CONTATO | Texto | Telefone |
| 🗺️ LINK_MAPS | Texto | Localização |

### Exemplo

| 🆔 ID | 🏢 Nome | 🌆 Cidade |
|---|---|---|
| 1 | PEV/SAMAE | Blumenau |

---

## ♻️ 2. materiais_aceitos

Armazena os materiais recebidos em cada ponto.

| Campo | Tipo | Descrição |
|:---|:---:|:---|
| 🆔 ID_MATERIAL | Inteiro | Identificador |
| 🔗 ID_PONTO | Inteiro | Chave estrangeira |
| 🧪 TIPO_MATERIAL_ACEITO | Texto | Material recebido |
| 📝 OBSERVAÇÃO | Texto | Informações adicionais |

### Relacionamento

```text
🔗 ID_PONTO → pontos_coleta.ID
```

### Cardinalidade

```text
1 📍 ponto_coleta ---- N ♻️ materiais_aceitos
```

---

## 📋 3. procedimentos_descarte

Armazena regras e orientações para descarte.

| Campo | Tipo | Descrição |
|:---|:---:|:---|
| 🆔 ID | Inteiro | Identificador |
| 🔗 ID_PONTO | Inteiro | Referência |
| 🕒 HORÁRIOS | Texto | Horário funcionamento |
| 📅 AGENDAMENTO | Texto | Necessidade de agendamento |
| 💲 CUSTO | Texto | Custos envolvidos |
| 🚚 MODALIDADE | Texto | Tipo de descarte |

### Relacionamento

```text
🔗 ID_PONTO → pontos_coleta.ID
```

### Cardinalidade

```text
1 📍 ponto_coleta ---- N 📋 procedimentos_descarte
```

---

## 📎 4. evidencia

Registra evidências e fontes da pesquisa.

| Campo | Tipo | Descrição |
|:---|:---:|:---|
| 🆔 ID | Inteiro | Identificador |
| 🔗 ID_PONTO | Inteiro | Referência |
| 📂 TIPO | Texto | Tipo de evidência |
| 📝 DESCRIÇÃO | Texto | Detalhes |
| 🔗 ARQUIVO/LINK | Texto | Link ou documento |
| 📅 DATA | Data | Data do registro |

### Relacionamento

```text
🔗 ID_PONTO → pontos_coleta.ID
```

### Cardinalidade

```text
1 📍 ponto_coleta ---- N 📎 evidencia
```

---

## 📈 5. analise_critica

Tabela destinada à avaliação qualitativa dos municípios.

| Campo | Tipo | Descrição |
|:---|:---:|:---|
| 🆔 ID | Inteiro | Identificador |
| 🌆 CIDADE | Texto | Município |
| 👍 FACILIDADE | Texto | Pontos positivos |
| ⚠️ DIFICULDADE | Texto | Problemas encontrados |
| 📢 DIVULGAÇÃO | Texto | Situação atual |
| 🚀 MELHORIAS | Texto | Sugestões futuras |

---

# 🧠 Modelo Relacional

```text
📍 PONTOS_COLETA
-----------------
ID (PK)
NOME
ENDEREÇO
BAIRRO
CIDADE
CONTATO
LINK_MAPS


♻️ MATERIAIS_ACEITOS
-----------------
ID_MATERIAL (PK)
ID_PONTO (FK)
TIPO_MATERIAL_ACEITO
OBSERVAÇÃO


📋 PROCEDIMENTOS_DESCARTE
-----------------
ID (PK)
ID_PONTO (FK)
HORÁRIOS
AGENDAMENTO
CUSTO
MODALIDADE


📎 EVIDENCIA
-----------------
ID (PK)
ID_PONTO (FK)
TIPO
DESCRIÇÃO
ARQUIVO/LINK
DATA


📈 ANALISE_CRITICA
-----------------
ID (PK)
CIDADE
FACILIDADE
DIFICULDADE
DIVULGAÇÃO
MELHORIAS
```

---

# ⚙️ Regras de Negócio

✅ Cada ponto de coleta pode aceitar vários materiais  

✅ Cada ponto pode possuir múltiplos procedimentos  

✅ Cada ponto pode possuir diversas evidências  

✅ Análises críticas são independentes  

✅ O sistema concentra informações sobre descarte e reciclagem

---

# 🚀 Melhorias Futuras

### Sugestões de evolução:

- 🌆 Criar tabela `cidade`
- 🏘️ Criar tabela `bairro`
- ♻️ Separar materiais em tabela própria
- 🕒 Padronizar horários
- 🧪 Criar categorias de resíduos
- 🌐 Validar URLs
- 📍 Inserir latitude/longitude
- 🔄 Adicionar status ativo/inativo

---

# 💾 Tecnologias Compatíveis

<div align="center">

| Banco |
|---|
| 🐬 MySQL |
| 🐘 PostgreSQL |
| 🪟 SQL Server |
| ⚡ SQLite |

</div>

---

<div align="center">

### 💚 Projeto voltado para gestão sustentável e descarte consciente ♻️

</div>
