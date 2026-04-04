# Análise Comparativa de LLMs em Questões Abertas da OAB

Este projeto compara o desempenho de três modelos de linguagem em questões abertas da OAB:

- GPT-5.3
- Claude Sonnet 4.6
- Gemini

A análise foi construída a partir de questões discursivas selecionadas do benchmark jurídico utilizado no relatório, com foco em comparar não apenas o conteúdo das respostas, mas também a forma como cada modelo classifica a dificuldade da questão, identifica a área jurídica e fundamenta a resposta com base legal.

## Objetivo

Avaliar qualitativamente o comportamento dos modelos em questões jurídicas abertas, considerando:

- classificação de nível da questão;
- aderência da área/categoria ao dataset;
- similaridade textual entre respostas;
- completude da base legal;
- índice de divergência por questão.

## Base de dados

As questões abertas foram selecionadas a partir do dataset:

- `question.jsonl` do projeto OAB Bench

No experimento documentado no relatório, foram analisadas as questões 1 a 10 do conjunto aberto.

## Metodologia

Como não existe gabarito oficial estruturado para validação das respostas abertas, a análise foi feita por **inferência comparativa** entre os modelos.

Cada modelo respondeu às questões a partir de um prompt padronizado em JSON, contendo campos como:

- `question`
- `model_answer`
- `difficulty_level`
- `classification`
- `justification`
- `area_of_expertise`
- `main_legal_reference`

### Métricas utilizadas

#### 1. Distribuição dos níveis por modelo
Compara quantas questões cada IA classificou como:

- Nível 1 — Estagiário
- Nível 2 — Analista
- Nível 3 — Juiz de Direito
- Nível 4 — Ministro STF/STJ

#### 2. Aderência à categoria do dataset
Compara o campo `area_of_expertise` com a categoria original da questão no dataset.

#### 3. Similaridade textual
Calcula a similaridade média entre os pares de modelos com base em `model_answer`.

#### 4. Completude da base legal
Cria um score heurístico a partir de elementos como:

- quantidade de artigos citados;
- menção a parágrafos e incisos;
- referência a Constituição, leis, súmulas, precedentes ou regimentos.

#### 5. Índice de divergência por questão
Combina:

- divergência de classificação;
- divergência de categoria;
- baixa similaridade textual.

## Principais resultados

Os principais achados do relatório foram:

- **Claude Sonnet 4.6** foi o modelo mais aderente ao dataset no critério de categoria;
- **Claude Sonnet 4.6** também apresentou a base legal mais completa;
- **GPT-5.3** se destacou pela objetividade e concisão;
- as respostas dos três modelos apresentaram **baixa similaridade textual**, indicando estilos argumentativos distintos;
- o índice de divergência permitiu identificar as questões mais sensíveis para análise qualitativa aprofundada.

### Métricas observadas no relatório

- Aderência à categoria:
  - Claude Sonnet 4.6: **10/10**
  - GPT-5.3: **9/10**
  - Gemini: **9/10**

- Similaridade média entre pares:
  - GPT-5.3 × Claude: **27,78%**
  - GPT-5.3 × Gemini: **15,69%**
  - Claude × Gemini: **17,15%**

- Completude média da base legal:
  - GPT-5.3: **5,225**
  - Claude Sonnet 4.6: **9,400**
  - Gemini: **8,525**

## Estrutura esperada do projeto

Uma estrutura sugerida para o repositório:

```bash
.
├── data/
│   ├── Dataset_extarido.txt
│   ├── respostas_gpt5.3_abertas.json
│   ├── respostas_claud.iaSonnet4.6_abertas.json
│   └── respostas_gemini_abertas.json
├── outputs/
│   ├── grafico_1_distribuicao_niveis.png
│   ├── grafico_2_aderencia_categoria.png
│   ├── grafico_3_similaridade_pares.png
│   ├── grafico_4_divergencia_questao.png
│   ├── grafico_5_completude_base_legal.png
│   ├── metricas_graficos_llms.xlsx
│   └── metricas_por_questao.csv
├── notebook.ipynb
├── analysis.py
└── README.md
