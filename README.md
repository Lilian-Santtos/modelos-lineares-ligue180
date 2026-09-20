# 📊 Análise da Evolução Temporal dos Registros do Ligue 180

[![Python](https://img.shields.io/badge/Python-3.x-blue?logo=python&logoColor=white)](https://www.python.org/)
[![Google Colab](https://img.shields.io/badge/Google%20Colab-Notebook-orange?logo=googlecolab&logoColor=white)](https://colab.research.google.com/)
[![Statsmodels](https://img.shields.io/badge/Statsmodels-Regressão%20Linear-lightgrey)](https://www.statsmodels.org/)
[![IESB](https://img.shields.io/badge/IESB-Ciência%20de%20Dados-red)](#)

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Lilian-Santtos/modelos-lineares-ligue180/blob/main/Modelos_Lineares_Trabalho_Final_VFINAL.ipynb)

## 📌 Sobre o projeto

Projeto acadêmico desenvolvido no curso de **Ciência de Dados e Inteligência Artificial do Centro Universitário IESB**, com o objetivo de aplicar conceitos de **Modelos Lineares** a dados públicos do serviço **Ligue 180 – Central de Atendimento à Mulher**.

A análise considera registros referentes ao período de **janeiro de 2022 a março de 2024** e busca investigar a existência de uma tendência temporal estatisticamente significativa na quantidade mensal de registros.

Além da regressão linear simples, foi estimado um modelo múltiplo incorporando variáveis indicadoras referentes aos trimestres do ano, permitindo avaliar se essas variáveis acrescentam capacidade explicativa à tendência temporal.

---

## 🎯 Objetivos

O projeto busca:

- analisar a evolução mensal dos registros do Ligue 180;
- verificar a associação entre tempo e quantidade de registros;
- estimar um modelo de regressão linear simples;
- estimar um modelo de regressão linear múltipla;
- avaliar possíveis efeitos associados aos trimestres do ano;
- comparar formalmente os modelos;
- verificar os principais pressupostos da regressão linear;
- identificar observações potencialmente influentes;
- avaliar a estabilidade dos resultados por meio de análise de sensibilidade.

---

## 🗂️ Base de dados

A base foi consolidada a partir de arquivos públicos disponibilizados pelo **Ligue 180**.

### Base original

| Característica | Resultado |
|---|---:|
| Registros | 1.299.357 |
| Variáveis | 62 |
| Período | Jan/2022 a Mar/2024 |

Para a modelagem estatística, os registros individuais foram agregados mensalmente, resultando em **27 observações**.

---

## 🔎 Variáveis utilizadas

| Variável | Descrição |
|---|---|
| `DATA_DE_CADASTRO` | Data em que o registro foi realizado |
| `MES` | Mês de referência do registro |
| `QUANTIDADE_REGISTROS` | Quantidade total de registros observados em cada mês |
| `TEMPO` | Sequência cronológica dos meses, de 1 a 27 |
| `TRIMESTRE` | Trimestre correspondente a cada observação |
| `T_2` | Variável indicadora do segundo trimestre |
| `T_3` | Variável indicadora do terceiro trimestre |
| `T_4` | Variável indicadora do quarto trimestre |

O primeiro trimestre foi utilizado como categoria de referência no modelo de regressão linear múltipla.

---

## 🧪 Metodologia

O desenvolvimento foi organizado nas seguintes etapas:

1. carregamento e consolidação das bases;
2. tratamento e verificação dos dados;
3. construção da base mensal;
4. análise exploratória;
5. cálculo da correlação de Pearson;
6. regressão linear simples;
7. regressão linear múltipla;
8. comparação entre modelos por teste F;
9. análise dos resíduos;
10. teste de Shapiro-Wilk;
11. teste de Breusch-Pagan;
12. estatística de Durbin-Watson;
13. Distância de Cook;
14. análise de sensibilidade.

Os modelos foram estimados pelo método dos **Mínimos Quadrados Ordinários (MQO)**.

---

## 📈 Principais resultados

### Correlação

A correlação de Pearson entre `TEMPO` e `QUANTIDADE_REGISTROS` foi:

**r = 0,8712**

O resultado indica uma associação linear positiva forte entre a passagem do tempo e a quantidade mensal de registros.

---

### Regressão Linear Simples

O modelo estimado apresentou aproximadamente:

$$
\hat{Y} = 35.251,03 + 919,52 \times TEMPO
$$

Principais resultados:

| Indicador | Resultado |
|---|---:|
| Coeficiente de `TEMPO` | 919,52 |
| R² | 0,759 |
| R² ajustado | 0,749 |
| Estatística F | 78,72 |
| p-valor de `TEMPO` | < 0,001 |

O avanço de um mês esteve associado, em média, a um aumento estimado de aproximadamente **920 registros mensais** durante o período analisado.

---

### Regressão Linear Múltipla

O modelo múltiplo incorporou as variáveis `T_2`, `T_3` e `T_4`.

| Indicador | Resultado |
|---|---:|
| R² | 0,794 |
| R² ajustado | 0,757 |
| Coeficiente de `TEMPO` | 918,63 |

Nenhuma das variáveis indicadoras dos trimestres apresentou significância estatística ao nível de 5%.

---

## ⚖️ Comparação entre os modelos

Foi utilizado um **teste F para modelos aninhados**.

| Indicador | Resultado |
|---|---:|
| Estatística F | ≈ 1,248 |
| p-valor | ≈ 0,3165 |

Como o p-valor foi superior a 0,05, não foram encontradas evidências de que a inclusão conjunta das variáveis referentes aos trimestres proporcionasse melhora estatisticamente significativa no ajuste.

Por esse motivo, o **modelo de regressão linear simples foi selecionado como o modelo mais parcimonioso**.

---

## 🔬 Diagnóstico do modelo selecionado

Os principais resultados dos diagnósticos foram:

| Diagnóstico | Resultado |
|---|---|
| Linearidade | Possível curvatura nos resíduos |
| Shapiro-Wilk | p = 0,2509 |
| Breusch-Pagan | p = 0,5582 |
| Durbin-Watson | 1,5097 |
| Distância de Cook | Mar/2024 = 0,183 |
| Limite de referência Cook | ≈ 0,148 |

Os testes não apresentaram evidências de violação das suposições de **normalidade** e **homocedasticidade**.

A estatística de Durbin-Watson indicou possível dependência temporal, considerada um ponto de atenção devido à natureza sequencial das observações.

Março de 2024 foi identificado como observação potencialmente influente.

---

## 🔁 Análise de sensibilidade

O modelo foi reestimado sem março de 2024.

| Indicador | Modelo original | Sem Mar/2024 |
|---|---:|---:|
| Coeficiente de `TEMPO` | 919,52 | 865,74 |
| R² | 0,7590 | 0,7325 |
| p-valor de `TEMPO` | < 0,001 | ≈ 2,50 × 10⁻⁸ |

Embora a retirada da observação tenha reduzido a magnitude do coeficiente temporal, a relação permaneceu positiva e estatisticamente significativa.

Assim, a conclusão principal não depende exclusivamente dessa observação.

---

## ✅ Conclusão

Os resultados fornecem evidências estatísticas de uma **tendência temporal positiva na quantidade mensal de registros realizados no Ligue 180** durante o período analisado.

O modelo de regressão linear simples mostrou-se mais parcimonioso e adequado para responder às hipóteses estabelecidas, embora tenham sido identificados pontos de atenção relacionados à possível não linearidade e à dependência temporal dos resíduos.

É importante destacar que a variável analisada corresponde à **quantidade de registros realizados no Ligue 180**.

Portanto, o crescimento observado não deve ser interpretado, isoladamente, como aumento da ocorrência real de violência contra as mulheres.

---

## 💻 Tecnologias utilizadas

- Python
- Google Colab
- Pandas
- NumPy
- Matplotlib
- Statsmodels
- SciPy

---

## ▶️ Reproduzir a análise

O notebook realiza automaticamente o download das mesmas bases públicas do Ligue 180 utilizadas na elaboração deste projeto.

Dessa forma, a análise pode ser reproduzida diretamente no Google Colab, sem necessidade de acesso ao Google Drive dos autores, download manual dos arquivos ou alteração dos caminhos de carregamento.

As cópias das bases disponibilizadas para execução correspondem às versões utilizadas originalmente no trabalho, contribuindo para a reprodutibilidade dos resultados.

Para executar o projeto, clique no botão abaixo:

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Lilian-Santtos/modelos-lineares-ligue180/blob/main/Modelos_Lineares_Trabalho_Final_VFINAL.ipynb)

---

## 📁 Estrutura do repositório

```text
modelos-lineares-ligue180/
│
├── README.md
├── Modelos_Lineares_Trabalho_Final_VFINAL.ipynb
└── Modelos de Regressão Linear - Análise da Evolução Temporal dos Registros do Ligue 180.pdf
```

## 📄 Relatório final

O relatório acadêmico completo pode ser acessado diretamente pelo link abaixo:

📄 [Abrir relatório final em PDF](https://github.com/Lilian-Santtos/modelos-lineares-ligue180/raw/refs/heads/main/Modelos%20de%20Regress%C3%A3o%20Linear%20-%20An%C3%A1lise%20da%20Evolu%C3%A7%C3%A3o%20Temporal%20dos%20Registros%20do%20Ligue%20180.pdf)

---

## 👩‍🎓👨‍🎓 Autores

**Lilian Santos Sousa**  
**Gedson Gonçalves da Silva**

Curso de **Ciência de Dados e Inteligência Artificial**  
Centro Universitário IESB  
Brasília – DF  
2026

---

## 📚 Fonte dos dados

BRASIL. **Central de Atendimento à Mulher – Ligue 180: base de dados**. Governo Federal.

Dados públicos disponíveis em:  
https://dados.gov.br/dados/conjuntos-dados/central-de-atendimento-a-mulher--ligue-180
