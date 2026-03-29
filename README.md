# Olympics Data Lake

Data Lake local com dados históricos e recentes dos Jogos Olímpicos, construído como projeto acadêmico para explorar conceitos de engenharia de dados com camadas **raw → bronze → gold**.

---

## Estrutura do Projeto

```
olympics-datalake/
│
├── README.md                        ← Este arquivo
├── metadata_schema.json             ← Schema técnico de metadados
│
├── raw/                             ← Dados brutos, sem transformação
│   ├── olympics_historico.csv       ← Resultados históricos 1896–2022 (316.834 registros)
│   ├── olympics_historico.json      ← Metadados
│   ├── olympics_paris2024.csv       ← Medalhas Paris 2024 (1.044 registros)
│   └── olympics_paris2024.json      ← Metadados
│
├── bronze/                          ← Dados integrados e limpos
│   ├── medalhas_1986_2024.csv       ← JOIN histórico + Paris 2024 (45.731 medalhas)
│   ├── medalhas_1986_2024.json
│   ├── modalidades_1986_2024.csv    ← Agregação por esporte/edição (1.138 registros)
│   ├── modalidades_1986_2024.json
│   ├── atletas_por_sexo.csv         ← Distribuição por gênero/disciplina
│   └── atletas_por_sexo.json
│
└── gold/                            ← Análises e visualizações finais
    ├── analise_medalhas/
    │   ├── medalhas_summary.csv     ← Quadro de medalhas Paris 2024 (92 países)
    │   ├── medalhas_plot.png        ← Gráfico top 15 países
    │   ├── notebook.ipynb           ← Jupyter Notebook completo
    │   └── metadata.json
    ├── analise_modalidades/
    │   ├── modalidades_plot.png     ← Top 10 modalidades históricas
    │   └── metadata.json
    └── analise_genero/
        ├── genero_plot.png          ← Medalhas por gênero
        └── metadata.json
```

---

## Fontes de Dados

| Dataset | Fonte | Período | Registros |
|---|---|---|---|
| `olympics_historico.csv` | Olympedia / Kaggle | 1896 – 2022 | 316.834 |
| `olympics_paris2024.csv` | Paris 2024 / Kaggle | Julho–Agosto 2024 | 1.044 |

---

## Arquitetura do Data Lake

### Camada `raw/`
Dados **brutos**, exatamente como foram coletados. Nenhuma transformação é aplicada. Cada arquivo possui um JSON de metadados descrevendo origem, campos e observações.

### Camada `bronze/`
Dados **integrados e normalizados**. As principais operações realizadas foram:
- Extração e descompressão do arquivo `.gz` histórico
- Normalização dos nomes de colunas entre as duas fontes
- **JOIN** (concatenação vertical) entre histórico e Paris 2024
- Agregações por modalidade, edição e gênero

### Camada `gold/`
**Análises prontas para consumo**: quadro de medalhas, gráficos comparativos e insights por gênero e modalidade. Todo o processo está documentado no `notebook.ipynb`.

---

## Apontamentos

- **EUA e China** empataram em ouros (40 cada) em Paris 2024 — EUA ficou em 1º por ter mais pratas (44 vs 27)
- **Japão** surpreendeu em 3º lugar com 20 medalhas de ouro
- **Paris 2024** foi a primeira edição com **paridade total de atletas** (50% feminino / 50% masculino)
- **Atletismo** é historicamente a modalidade com maior número de atletas participantes

---
