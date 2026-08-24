# Mega-Sena MVP

Exercício de prática com Google Colab e GitHub: reproduz a base de dados sintética do projeto [`andrelmsunb/PredicaoMegasena`](https://github.com/andrelmsunb/PredicaoMegasena) e monta, em cima dela, um pipeline mínimo de análise exploratória + um modelo de machine learning.

## Objetivo

Praticar o fluxo completo de um notebook de ciência de dados — geração/carga de base, EDA, preparo de features, treino e avaliação de um modelo — usando um problema simples e com dados abertos de gerar (nenhuma dependência externa, nenhuma chave de API).

Não é uma ferramenta para prever resultados da Mega-Sena. A Mega-Sena é um sorteio aleatório: nenhuma análise estatística ou modelo de machine learning muda a probabilidade de acerto em um sorteio real. Esse projeto é só material de estudo.

## Sobre a base de dados

O repositório original não consome uma base pública — ele **gera** uma base sintética dentro do próprio notebook, com semente fixa (`np.random.seed(42)`), simulando 2.900 concursos com um conjunto de "números quentes" levemente mais prováveis. Este projeto reproduz exatamente essa mesma lógica de geração (mesma classe, mesma semente), então os dados usados aqui são idênticos aos do projeto de referência.

Colunas geradas por concurso:

- `numero1` a `numero6` — os 6 números sorteados
- `soma_numeros`, `numeros_pares`, `numeros_impares`, `numeros_consecutivos`, `diff_max_min`
- `dezena_1_10` ... `dezena_51_60` — contagem de números por faixa de dezena
- `termina_0` ... `termina_9` — contagem de números por algarismo final
- `ganhadores`, `premio`, `apostas` — valores simulados, sem relação com dados reais

## Estrutura do notebook

`MegaSena_MVP.ipynb`

1. **Geração da base** — classe `MegaSenaDataCollector`, idêntica à do repositório original.
2. **Análise exploratória** — frequência dos números, distribuição da soma (com teste de normalidade Shapiro-Wilk), paridade, números consecutivos, distribuição por dezena e por terminação, correlação entre variáveis.
3. **Modelo preditivo** — `RandomForestRegressor` (scikit-learn) treinado para estimar `soma_numeros` a partir das demais estatísticas do concurso, com padronização (`StandardScaler`), split treino/teste e métricas MAE, MSE e R².
4. **Sugestão final** — amostragem de 6 números ponderada pela frequência histórica simulada, apresentada com o mesmo disclaimer do item acima.

## Como rodar

1. Suba `MegaSena_MVP.ipynb` no [Google Colab](https://colab.research.google.com/) (ou abra localmente com Jupyter).
2. Execute as células em ordem — não há downloads externos nem configuração adicional.

## Dependências

`numpy`, `pandas`, `matplotlib`, `seaborn`, `scipy`, `scikit-learn` — todas já vêm pré-instaladas no Google Colab.

## Referência

Projeto original: [andrelmsunb/PredicaoMegasena](https://github.com/andrelmsunb/PredicaoMegasena)
