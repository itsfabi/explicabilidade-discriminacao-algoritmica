# explicabilidade-discriminacao-algoritmica
Código-fonte do Trabalho de Conclusão de Curso (TCC) do curso de Análise e Desenvolvimento de Sistemas da **Fatec Campinas**.

- **Autores:** Fabiana Watanabe e Gustavo Meneses Ruegenberg Rodrigues
- **Orientadora:** Profa. Ana Claudia das Neves Silva
- **Ano:** 2026

## Sobre o estudo

O trabalho investiga se um modelo de *Machine Learning* treinado para apoiar a seleção de candidatos reproduz discriminação por gênero, raça ou idade, e se técnicas de Inteligência Artificial Explicável (XAI) conseguem tornar esse comportamento visível.

Foi treinado um modelo **Random Forest** (100 árvores, `max_depth=10`, `random_state=42`) para prever a aprovação de candidatos. Em seguida, o modelo foi analisado com:

- **SHAP** (explicações globais e individuais);
- **LIME** (comparação de pares de candidatos com mesmo cargo e mesma idade, diferindo apenas no gênero);
- **métricas de equidade** (impacto desproporcional, regra dos quatro quintos e diferença de paridade demográfica).

### Principais resultados (conjunto de teste, 2.000 registros)

| Métrica | Valor |
|---|---|
| Acurácia | 77,1% |
| Precisão | 78,9% |
| Revocação (*recall*) | 72,3% |
| F1-score | 75,4% |
| AUC-ROC | 0,842 |

Nas previsões do modelo, a razão de aprovação entre mulheres e homens foi de **0,208**, abaixo do limite de 0,80 da regra dos quatro quintos. A variável `Gender_Male` foi a de maior importância média no SHAP (0,1019). Os detalhes e as limitações estão no texto do TCC.

## Base de dados

- **Fonte:** *Recruitment Dataset*, disponível no Kaggle (Nellore, 2024): https://www.kaggle.com/datasets/surendra365/recruitement-dataset
- **Tamanho:** 10.000 registros e 9 colunas.
- **Natureza:** a base aparenta ser sintética (poucos nomes distintos entre os registros), o que limita a generalização dos resultados para processos seletivos reais.
- **Arquivo usado:** `recruitment_data_fixed.csv`, versão corrigida da base original. As correções aplicadas estão descritas na seção de Metodologia do TCC.

> Antes de reutilizar a base, consulte a licença na página original do Kaggle.

## Estrutura do repositório

```
.
├── 00_configuracao_ambiente.ipynb   # instalação e verificação das bibliotecas
├── 01_preprocessamento.ipynb        # leitura, limpeza e codificação dos dados
├── 02_treino_modelo.ipynb           # divisão treino/teste e treino do Random Forest
├── 03_shap.ipynb                    # análise SHAP (global e individual)
├── 04_analise_idade.ipynb           # análise por faixa etária
├── 05_lime.ipynb                    # análise LIME em pares de candidatos
├── 06_metricas_equidade.ipynb       # impacto desproporcional e paridade demográfica
├── recruitment_data_fixed.csv       # base de dados corrigida
└── dados/                           # arquivos gerados pelos notebooks (figuras, divisões)
```

## Como reproduzir

1. Clone ou baixe este repositório.
2. Crie um ambiente Python e instale as dependências (versões no Quadro 2 do TCC):
   ```bash
   pip install pandas numpy scikit-learn shap lime matplotlib seaborn scipy jupyter
   ```
3. Mantenha o arquivo `recruitment_data_fixed.csv` na mesma pasta dos notebooks.
4. Execute os notebooks **na ordem numérica** (00 a 06). Cada notebook usa arquivos gerados pelos anteriores.
5. Todos os procedimentos aleatórios usam a semente **42**, mas os pesos do LIME podem variar levemente entre execuções.

## Versões das bibliotecas

| Biblioteca | Versão |
|---|---|
| Python | 3.14.2 |
| pandas | 3.0.6 |
| numpy | 2.5.3 |
| scikit-learn | 1.9.1 |
| shap | 0.52.0 |
| lime | 0.20.1 |
| matplotlib | 3.11.2 |
| scipy | 1.18.1 |

## Aviso

Este código tem finalidade acadêmica. Os resultados refletem uma base de dados aparentemente sintética e não devem ser usados para avaliar ou apoiar decisões reais de contratação.
