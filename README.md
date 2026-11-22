# Painel Rosa - Voluntariado

[Português](#português) | [English](#english)

---

## Português

### Sobre o Projeto

Este repositório reúne e organiza as contribuições voluntárias realizadas para a etapa de **coleta de dados públicos** do projeto **Painel Rosa** — iniciativa voluntária de análise de dados voltada ao tema de **câncer de mama e saúde da mulher (Outubro Rosa)**.

O foco deste repositório é servir como **registro histórico e portfólio organizado** dos notebooks de extração de indicadores demográficos e socioeconômicos (municípios brasileiros, população, IDHM e rendimento) a partir de APIs do **IBGE** e da plataforma **Base dos Dados** (Atlas do Desenvolvimento Humano - PNUD). Os outputs originais executados foram preservados nos notebooks como amostra visual dos dados coletados.

### Estrutura do Repositório

```text
Painel-Rosa-Voluntariado/
├── notebooks/
│   ├── coleta_municipios_ibge.ipynb   # Códigos e nomes de municípios brasileiros (IBGE)
│   ├── coleta_populacao_ibge.ipynb    # População residente por sexo e faixa etária (Censo/IBGE)
│   ├── coleta_idhm_adh.ipynb          # IDHM municipal via Base dos Dados (Atlas/PNUD)
│   └── coleta_renda_pnad.ipynb        # Série mensal de rendimento médio no Brasil (PNAD Contínua/IBGE)
├── .gitignore
├── README.md
└── requirements.txt
```

### Descrição dos Notebooks

| Notebook | Tema / Indicador | Fonte / API | Escopo Geográfico e Temporal | Colunas Principais | Observações |
| :--- | :--- | :--- | :--- | :--- | :--- |
| [coleta_municipios_ibge.ipynb](notebooks/coleta_municipios_ibge.ipynb) | Códigos e nomes de municípios e UFs | API de Localidades do IBGE (`v1`) | 27 UFs (5.570 municípios) | `id_uf`, `UF`, `id_municipio`, `nome_municipio` | Base auxiliar para cruzamento por código IBGE |
| [coleta_populacao_ibge.ipynb](notebooks/coleta_populacao_ibge.ipynb) | População residente por sexo e faixa etária | API de Agregados do IBGE (`v3` — Agregado `205`, Variável `93`) | Municípios (`N6[all]`), Censo `1991` (26.946 registros) | `codigo_sexo`, `valor_sexo`, `codigo_local`, `nome_local`, `ano`, `populacao`, `faixa_idade` | Criado em colaboração por `@Mariana` e `@Heber`; inclui URLs mapeadas para Censo 2010 |
| [coleta_idhm_adh.ipynb](notebooks/coleta_idhm_adh.ipynb) | Índice de Desenvolvimento Humano Municipal (IDHM) | Base dos Dados (`mundo_onu_adh.municipio`) | Municípios brasileiros, censos `1991–2010` (16.695 registros) | `ano`, `id_municipio`, `idhm` (tabela completa inclui `idhm_e`, `idhm_l`, `idhm_r` e demais indicadores) | Requer `billing_project_id` válido do Google Cloud Platform |
| [coleta_renda_pnad.ipynb](notebooks/coleta_renda_pnad.ipynb) | Rendimento médio mensal | API de Agregados do IBGE (`v3` — Agregado `6387`, Variável `5935`) | Brasil (`N1[all]`), série mensal `2012/03` a `2022/11` (129 registros) | `codigo_local`, `nome_local`, `ano`, `valor`, `mes` | Converte o período `YYYYMM` em colunas separadas de `ano` e `mes` |

### Fontes e Referências Mapeadas

Além das consultas executadas diretamente nos notebooks, o levantamento inicial do projeto mapeou as seguintes tabelas e endpoints públicos de referência:

- **API de Localidades IBGE (v1) — Municípios por UF**:
  - `https://servicodados.ibge.gov.br/api/v1/localidades/estados/.../municipios`
- **SIDRA / API de Agregados IBGE (v3)**:
  - **Agregado `205` (Variável `93`)**: População residente por sexo e grupos de idade (Censo 1991) — utilizada em `coleta_populacao_ibge.ipynb`.
  - **Agregado `200` (Variável `93`)**: População residente por sexo, situação do domicílio e grupos de idade (Censo 2010) — mapeada em `coleta_populacao_ibge.ipynb`.
  - **Agregado `3974` (Variável `3948`)**: Valor do rendimento nominal médio mensal domiciliar per capita das pessoas de 10 anos ou mais de idade (Censo 2010) — mapeada em `coleta_populacao_ibge.ipynb`.
  - **Agregado `6387` (Variável `5935`)**: Rendimento médio real habitual (PNAD Contínua Mensal) — utilizada em `coleta_renda_pnad.ipynb`.
  - **Tabela SIDRA `5938`**: Produto Interno Bruto dos Municípios (PIB municipal) — referência registrada originalmente nas notas do projeto (`https://sidra.ibge.gov.br/tabela/5938`).
- **Base dos Dados — Atlas do Desenvolvimento Humano (`mundo_onu_adh.municipio`)**:
  - Dados municipais de Longevidade, Educação, Renda e IDHM (PNUD / IPEA / FJP).

### Como Executar

1. Crie e ative um ambiente virtual Python (recomendado Python 3.9+):
   ```bash
   python -m venv .venv
   # Windows (PowerShell)
   .venv\Scripts\Activate.ps1
   # Linux/macOS
   source .venv/bin/activate
   ```
2. Instale as dependências:
   ```bash
   pip install -r requirements.txt
   ```
3. Inicie o Jupyter Notebook ou JupyterLab:
   ```bash
   jupyter notebook
   ```
4. **Nota sobre o notebook de IDHM (`coleta_idhm_adh.ipynb`)**: antes de executar a célula `bd.read_table(...)`, substitua `"SEU_PROJETO_GCP"` pelo ID de um projeto válido no Google Cloud Platform com faturamento/BigQuery habilitado para uso da biblioteca `basedosdados`.

### Créditos

- Contribuições voluntárias para a iniciativa **Painel Rosa**.
- Colaboração em `coleta_populacao_ibge.ipynb`: créditos originais mantidos para **@Mariana** e **@Heber**.

---

## English

### About the Project

This repository collects and organizes volunteer contributions made to the **public data collection stage** of **Painel Rosa** — a volunteer data analytics initiative focused on **breast cancer and women's health (Pink October / Outubro Rosa)**.

The goal of this repository is to serve as a **clean, well-documented historical portfolio record** of the notebooks used to extract demographic and socioeconomic indicators (Brazilian municipalities, population, Municipal HDI / IDHM, and income) from **IBGE** APIs and **Base dos Dados** (Human Development Atlas - UNDP). Original executed outputs have been preserved inside the notebooks as visual samples of the extracted datasets.

### Repository Structure

```text
Painel-Rosa-Voluntariado/
├── notebooks/
│   ├── coleta_municipios_ibge.ipynb   # Brazilian municipality codes and names (IBGE)
│   ├── coleta_populacao_ibge.ipynb    # Resident population by sex and age group (Census/IBGE)
│   ├── coleta_idhm_adh.ipynb          # Municipal HDI (IDHM) via Base dos Dados (UNDP)
│   └── coleta_renda_pnad.ipynb        # Monthly average income series in Brazil (PNAD Contínua/IBGE)
├── .gitignore
├── README.md
└── requirements.txt
```

### Notebooks Overview

| Notebook | Topic / Indicator | Data Source / API | Geographic & Time Scope | Key Columns | Notes |
| :--- | :--- | :--- | :--- | :--- | :--- |
| [coleta_municipios_ibge.ipynb](notebooks/coleta_municipios_ibge.ipynb) | Municipality and state (UF) codes & names | IBGE Localidades API (`v1`) | 27 Brazilian states (5,570 municipalities) | `id_uf`, `UF`, `id_municipio`, `nome_municipio` | Lookup table for joining datasets by IBGE code |
| [coleta_populacao_ibge.ipynb](notebooks/coleta_populacao_ibge.ipynb) | Resident population by sex and age group | IBGE Agregados API (`v3` — Aggregate `205`, Variable `93`) | Municipalities (`N6[all]`), `1991` Census (26,946 rows) | `codigo_sexo`, `valor_sexo`, `codigo_local`, `nome_local`, `ano`, `populacao`, `faixa_idade` | Authored collaboratively by `@Mariana` and `@Heber`; includes mapped 2010 Census endpoints |
| [coleta_idhm_adh.ipynb](notebooks/coleta_idhm_adh.ipynb) | Municipal Human Development Index (IDHM) | Base dos Dados (`mundo_onu_adh.municipio`) | Brazilian municipalities, `1991–2010` censuses (16,695 rows) | `ano`, `id_municipio`, `idhm` (full table includes `idhm_e`, `idhm_l`, `idhm_r`, etc.) | Requires a valid Google Cloud Platform `billing_project_id` |
| [coleta_renda_pnad.ipynb](notebooks/coleta_renda_pnad.ipynb) | Monthly average income | IBGE Agregados API (`v3` — Aggregate `6387`, Variable `5935`) | Brazil (`N1[all]`), monthly series `2012/03` to `2022/11` (129 rows) | `codigo_local`, `nome_local`, `ano`, `valor`, `mes` | Parses `YYYYMM` period strings into `ano` and `mes` columns |

### Mapped Data Sources & References

In addition to the queries executed in the notebooks, the project's initial data-scouting phase mapped the following public endpoints and reference tables:

- **IBGE Localidades API (v1) — Municipalities by State (UF)**:
  - `https://servicodados.ibge.gov.br/api/v1/localidades/estados/.../municipios`
- **SIDRA / IBGE Agregados API (v3)**:
  - **Aggregate `205` (Variable `93`)**: Resident population by sex and age groups (1991 Census) — used in `coleta_populacao_ibge.ipynb`.
  - **Aggregate `200` (Variable `93`)**: Resident population by sex, urban/rural status, and age groups (2010 Census) — mapped in `coleta_populacao_ibge.ipynb`.
  - **Aggregate `3974` (Variable `3948`)**: Mean nominal monthly household income per capita for people aged 10+ (2010 Census) — mapped in `coleta_populacao_ibge.ipynb`.
  - **Aggregate `6387` (Variable `5935`)**: Average real habitual earnings (Monthly PNAD Contínua) — used in `coleta_renda_pnad.ipynb`.
  - **SIDRA Table `5938`**: Municipal Gross Domestic Product (PIB dos Municípios) — originally recorded in the project notes (`https://sidra.ibge.gov.br/tabela/5938`).
- **Base dos Dados — Human Development Atlas (`mundo_onu_adh.municipio`)**:
  - Municipal Longevity, Education, Income, and IDHM indicators (UNDP / IPEA / FJP).

### How to Run

1. Create and activate a Python virtual environment (Python 3.9+ recommended):
   ```bash
   python -m venv .venv
   # Windows (PowerShell)
   .venv\Scripts\Activate.ps1
   # Linux/macOS
   source .venv/bin/activate
   ```
2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
3. Launch Jupyter Notebook or JupyterLab:
   ```bash
   jupyter notebook
   ```
4. **Note on `coleta_idhm_adh.ipynb`**: before running `bd.read_table(...)`, replace `"SEU_PROJETO_GCP"` with a valid Google Cloud Platform billing project ID enabled for BigQuery / `basedosdados`.

### Credits

- Volunteer data contributions to the **Painel Rosa** initiative.
- Collaboration on `coleta_populacao_ibge.ipynb`: original credits preserved for **@Mariana** and **@Heber**.
