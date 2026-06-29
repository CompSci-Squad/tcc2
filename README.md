# TCC2 — Pré-processamento FRED-MD

Notebook de pré-processamento do dataset **FRED-MD** (McCracken & Ng, 2016) para indução de estacionariedade nas 128 séries macroeconômicas mensais.

## Conteúdo

| Arquivo | Descrição |
|---|---|
| `fred_md_stationarity.ipynb` | Notebook principal: leitura, transformação e z-score |

> Os arquivos CSV (`current.csv`, `fred_md_transformed.csv`) **não estão versionados**. Obtenha `current.csv` diretamente no [FRED-MD](https://research.stlouisfed.org/econ/mccracken/fred-databases/).

## Transformações aplicadas

Seguindo o **Appendix A** de McCracken & Ng (2016):

| tcode | Transformação |
|---|---|
| 1 | Nível (sem transformação) |
| 2 | Primeira diferença: Δxₜ |
| 3 | Segunda diferença: Δ²xₜ |
| 4 | Log: ln(xₜ) |
| 5 | Primeira diferença do log: Δln(xₜ) |
| 6 | Segunda diferença do log: Δ²ln(xₜ) |
| 7 | Diferença da taxa de crescimento: Δ(xₜ/xₜ₋₁ − 1) |

## Como rodar

### Pré-requisitos

```bash
pip install pandas numpy jupyter
```

### Passos

1. Baixe `current.csv` do FRED-MD e coloque na raiz do projeto.
2. Abra o notebook:
   ```bash
   jupyter notebook fred_md_stationarity.ipynb
   ```
3. Execute todas as células em ordem (`Run All`).
4. O arquivo `fred_md_transformed.csv` será gerado na mesma pasta.

## Referência

McCracken, M. W., & Ng, S. (2016). FRED-MD: A monthly database for macroeconomic research. *Journal of Business & Economic Statistics*, 34(4), 574–589.
