# TCC2 — Agrupamento de séries do FRED-MD

Trabalho do grupo CICD06. Agrupamos as séries macroeconômicas mensais do FRED-MD (McCracken e Ng, 2016) com K-Means e caracterizamos cada grupo por regressão contra 6 variáveis de referência. O pipeline segue Santos et al. (2021). Cada objeto agrupado é uma série inteira, não uma observação mensal.

## Estrutura

| Pasta/arquivo | Conteúdo |
|---|---|
| `fred_md_data_preparation.ipynb` | Notebook com o pipeline completo e as análises de robustez |
| `dados/` | Painel bruto do FRED-MD (vintage 2026-04, `2026-04-MD.csv`) |
| `resultados/tabelas/` | CSVs gerados pelo notebook (clusters, regressões, VIF, bootstrap, Ward) |
| `resultados/figuras/` | Figuras geradas pelo notebook (scree, clusters, heatmaps, rede, dendrograma) |
| `artigos/tcc-conic-2/` | Artigo do CONIC em LaTeX (`main.tex`, seções, tabelas, figuras) |
| `docs/` | Diretrizes do orientador, regulamento do CONIC, artigo de referência, roteiro dos próximos meses |

## Pipeline

1. Preparação: transformação por `tcode`, corte em 1965-01, imputação das células ausentes e z-score. As 6 séries de referência saem do painel clusterizado, ficando 118 séries.
2. Fatorabilidade: Bartlett e KMO.
3. Número de grupos: PCA com 70% de variância acumulada, que dá k = 19.
4. Agrupamento: K-Means (k-means++, 20 inicializações) sobre as 118 séries.
5. Caracterização: regressão OLS do centróide de cada cluster contra as 6 variáveis, com erro-padrão HAC (Newey-West) e diagnóstico de resíduos (Durbin-Watson, Breusch-Godfrey).
6. Rotulagem econômica dos clusters.

Robustez e extras (roteiro de setembro): VIF das variáveis de referência, block bootstrap com índice de Jaccard para os clusters 3, 4, 14 e 18, estatística descritiva dos centróides, rede de correlação e comparação com agrupamento hierárquico (Ward).

## Como rodar

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
python -m ipykernel install --user --name=tcc2 --display-name "Python (tcc2)"
jupyter lab fred_md_data_preparation.ipynb
```

Selecione o kernel **Python (tcc2)** e rode as células em ordem. O notebook lê `dados/2026-04-MD.csv` e grava tudo em `resultados/`.

## Artigo

```bash
cd artigos/tcc-conic-2
pdflatex main.tex && bibtex main && pdflatex main.tex && pdflatex main.tex
```

## Referências

- McCracken, M. W. e Ng, S. (2016). FRED-MD: a monthly database for macroeconomic research. *Journal of Business & Economic Statistics*, 34(4), 574-589.
- Santos, D. R. et al. (2021). Clusterização de ativos e suas relações com variáveis macroeconômicas e índices financeiros. *Research, Society and Development*, 10(2).
