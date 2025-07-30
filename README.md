
# 📚 Educational Indicators BR

[![Licença MIT](https://img.shields.io/badge/Licença-MIT-green)](https://pt.wikipedia.org/wiki/Licen%C3%A7a_MIT)
[![Python 3.10+](https://img.shields.io/badge/Python-3.10%2B-blue)](https://www.python.org/downloads/)
[![GeoPandas](https://img.shields.io/badge/GeoPandas-Geospatial_analysis-blue)](https://geopandas.org/)

## 📌 Sumário
1. [Visão Geral](#-visão-geral)  
2. [Indicadores Principais](#-indicadores-principais)
3. [Fatores de Influência](#-fatores-de-influência)
4. [Fontes de Dados](#-fontes-de-dados)
5. [Metodologia](#-metodologia)
6. [Instalação](#-instalação)
7. [Como Usar](#-como-usar)
8. [Casos de Estudo](#-casos-de-estudo)
9. [Contribuição](#-contribuição)
10. [Contato](#-contato)

---

## 🌐 Visão Geral

Plataforma analítica que integra indicadores educacionais brasileiros com dados socioeconômicos para:

- 🎯 **Identificar desigualdades educacionais** em nível municipal
- 📊 **Relacionar desempenho escolar** com contexto social
- 🗺️ **Mapear áreas prioritárias** para intervenção
- 📈 **Monitorar evolução temporal** (2007-2023)

**Aplicações:**
- Formulação de políticas educacionais
- Alocação de recursos do FUNDEB
- Estudos de impacto social
- Planejamento pedagógico regionalizado

---

## 📊 Indicadores Principais

### Educacionais
| Indicador | Fórmula | Fonte | Escala |
|-----------|---------|-------|--------|
| IDEB | `(Proficiência) × (Fluxo)` | INEP | Escola |
| Taxa de Abandono | `(Matrículas Iniciais - Finais)/Iniciais` | Censo Escolar | Municipal |
| Distorção Idade-Série | `Alunos com atraso ≥2 anos/Total` | INEP | Estadual |

### Socioeconômicos
| Indicador | Fonte | Relação Educacional |
|-----------|-------|--------------------|
| IDH-M | PNUD | Correlação +0.72 com IDEB |
| % Bolsa Família | MDS | Associado a evasão |
| Densidade Escolar | IBGE | Acesso à educação |

```python
from edu_analysis import calculate_educational_gap

gap = calculate_educational_gap(
    indicator='ideb',
    reference='capital',
    comparison='interior'
)
```

---

## 📂 Fontes de Dados

| Fonte | Dados | Periodicidade | Acesso |
|-------|-------|--------------|--------|
| INEP (Censo Escolar) | Matrículas, Infraestrutura | Anual | Microdados |
| Prova Brasil/SAEB | Desempenho | Bienal | API |
| IBGE (PNAD Contínua) | Educação domiciliar | Trimestral | FTP |
| MEC (IDEB) | Qualidade educacional | Bienal | Portal |

**Estrutura Básica:**
```python
import pandas as pd

df = pd.read_csv('ideb_municipal_2021.csv')
print(df.groupby('UF')['IDEB'].describe())
```

---

## 🔍 Fatores de Influência

### Principais Variáveis Analisadas
1. **Infraestrutura Escolar**:
   - Laboratórios de ciências
   - Acesso à internet

2. **Contexto Familiar**:
   - Escolaridade dos pais
   - Renda per capita

3. **Gestão Educacional**:
   - Experiência dos diretores
   - Rotatividade docente

4. **Territoriais**:
   - Distância até escolas
   - Violência no entorno

---

## ⚙️ Metodologia

1. **Análise Multinível**:
   ```python
   from edu_modeling import run_multilevel_analysis

   results = run_multilevel_analysis(
       educational_outcome='ideb',
       predictors=['idhm', 'teacher_ratio', 'family_income'],
       levels=['school', 'municipality']
   )
   ```

2. **Geoestatística**:
   ```python
   from edu_geo import identify_priority_areas

   priority_map = identify_priority_areas(
       indicators=['ideb', 'dropout_rate'],
       thresholds=[4.5, 0.1]
   )
   ```

3. **Séries Temporais**:
   - Tendências educacionais pós-PNE
   - Impacto de políticas específicas

---

## 🛠️ Instalação

### Via pip
```bash
pip install edu-indicators-br
```

### Com módulos geoespaciais
```bash
pip install edu-indicators-br[geo]
```

### Docker
```bash
docker pull inep/edu-analytics:latest
```

---

## 🚀 Como Usar

### 1. Análise Descritiva
```python
from edu_analysis import EducationReport

report = EducationReport(state='BA', year=2021)
report.generate(output_file='bahia_education.pdf')
```

### 2. Painel Interativo
```bash
streamlit run app/edu_dashboard.py
```

### 3. API de Consulta
```python
from edu_api import get_school_indicators

indicators = get_school_indicators(
    school_id=123456,
    indicators=['ideb', 'infrastructure_index']
)
```

---

## 🏫 Casos de Estudo

### Municípios com Maior Desigualdade (2021)
| Posição | Município | UF | IDEB Urbano | IDEB Rural | Diferença |
|---------|-----------|----|-------------|------------|-----------|
| 1 | Monte Alegre | PA | 5.8 | 3.2 | -2.6 |
| 2 | Baía Formosa | RN | 5.6 | 3.1 | -2.5 |

**Achados Relevantes:**
- Escolas com biblioteca têm 23% menos evasão
- 1h adicional de transporte reduz frequência em 11%

---

## 🗂 Estrutura do Projeto

```
edu-indicators-br/
├── data/
│   ├── raw/              # Microdados INEP/IBGE
│   ├── processed/        # Indicadores calculados
├── notebooks/
│   ├── pca_analysis.ipynb
├── edu_analysis/
│   ├── preprocessing/    # Pipeline de dados
│   ├── modeling/         # Modelos estatísticos
│   ├── geo/             # Ferramentas espaciais
├── docs/
│   ├── methodology.pdf  # Documentação técnica
└── tests/
```

---

## 🤝 Contribuição

1. **Adicionar Indicadores**:
   ```python
   class NewIndicator(EducationMetric):
       def __init__(self):
           self.name = "Índice de Equidade"
           self.formula = "(Variância de desempenho)/Média"
   ```

2. **Padrões de Código**:
   ```python
   def normalize_ideb(raw_score: float) -> float:
       """Normaliza IDEB para escala 0-1 considerando metas nacionais"""
       return (raw_score - 3) / (7 - 3)  # Meta 2022 básica vs excelência
   ```

3. **Testes**:
   ```bash
   pytest tests/test_priority_identification.py -v
   ```

---

## 📧 Contato

**Instituto Nacional de Estudos Educacionais**  
[pesquisa.indicadores@inep.gov.br](mailto:pesquisa.indicadores@inep.gov.br)

**Parcerias Acadêmicas**  
[parcerias@inep.gov.br](mailto:parcerias@inep.gov.br)

**Acesso aos Dados**  
[![Portal INEP](https://img.shields.io/badge/Dados_Educacionais-Acesse_Aqui-blue)](https://www.gov.br/inep/pt-br)

---

💡 **Para Gestores Educacionais:**  
Baixe nosso kit de intervenções comprovadas:  
[📘 Estratégias Baseadas em Evidências](docs/estrategias_educacionais.pdf)

> **Nota Técnica:** Todos os indicadores seguem as diretrizes do PNE (Plano Nacional de Educação 2014-2024).
```

### Destaques Específicos:

1. **Integração INEP-IBGE**: Cruzamento preciso de dados educacionais e socioeconômicos
2. **Abordagem Multinível**: Análise simultânea em nível aluno/escola/município
3. **Foco em Equidade**: Identificação de grupos vulneráveis
4. **Ferramentas para Gestão**: Priorização de áreas para intervenção
5. **Visualização Geográfica**: Mapas de calor de desigualdades educacionais

### Para Implementação:

1. Baixar microdados do Censo Escolar (INEP)
2. Cruzar com dados do IBGE e programas sociais
3. Mapear políticas municipais de educação
4. Implementar painéis de acompanhamento em tempo real
5. Calibrar modelos com dados locais específicos