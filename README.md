# Definição de Experimento: Análise de Estratégias de Release e Qualidade de Código

## 1. Identificação básica

### 1.1 Título do experimento
Análise Comparativa de Repositórios com Releases Rápidos e Lentos: Implicações para a Qualidade do Código.

### 1.2 ID / código
*Não informado no documento original.* (Referência interna sugerida: Artigo PUC-Minas).

### 1.3 Versão do documento e histórico de revisão
* **Versão Atual:** Publicação Final (Artigo Acadêmico).
* **Histórico:** O estudo baseou-se em mineração de dados inicial, seguida de filtragem e processamento final com análise estática para a redação do artigo.

### 1.4 Datas (criação, última atualização)
*Não informadas explicitamente.* O estudo utiliza referências bibliográficas até o ano de 2019.

### 1.5 Autores (nome, área, contato)
* **Alfredo L. Vieira** (Departamento de Engenharia de Software e Sistemas da Informação - PUC-Minas).
* **Bruno E. Gomes de Azevedo** (Departamento de Engenharia de Software e Sistemas da Informação - PUC-Minas).
* **Estevão de F. Rodrigues** (Departamento de Engenharia de Software e Sistemas da Informação - PUC-Minas).
* **Vinícius S. de Oliveira** (Departamento de Engenharia de Software e Sistemas da Informação - PUC-Minas).

### 1.6 Responsável principal (PI / dono do experimento)
Grupo de pesquisa da Pontifícia Universidade Católica de Minas Gerais (PUC-Minas).

### 1.7 Projeto / produto / iniciativa relacionada
Pesquisa acadêmica sobre Engenharia de Software, focada em estratégias de *release* (lançamento) e qualidade de software em projetos *open-source*.

---

## 2. Contexto e problema

### 2.1 Descrição do problema / oportunidade
Gerentes de projeto frequentemente enfrentam dúvidas sobre qual estratégia de lançamento adotar, precisando avaliar os *tradeoffs* entre estratégias de lançamento rápido (*rapid release*) e lento (*slow release*). Uma decisão equivocada pode levar a custos elevados de manutenção, insatisfação e perda de competitividade. O estudo busca esclarecer como essas estratégias impactam a qualidade final do produto.

### 2.2 Contexto organizacional e técnico
* **Ambiente:** Projetos *open-source* hospedados no GitHub.
* **Amostra:** 1.400 repositórios minerados (Top stars, >50 forks, >19 colaboradores).
* **Tecnologias/Ferramentas:** API GraphQL do GitHub para mineração, scripts em Python para automação e filtragem, e SonarQube para análise estática de código.

### 2.3 Trabalhos e evidências prévias (internos e externos)
* **RapidRelease - A Dataset of Projects... (Joshi & Chimalakonda, 2019):** Forneceu a definição de *rapid release* (ciclo médio entre 5 e 35 dias) e o dataset base.
* **Modern Release Engineering in a Nutshell:** Base para entendimento das fases do pipeline de engenharia de release.
* **Systematic literature review on... Agile Release Engineering:** Indicou que releases rápidas melhoram eficiência, mas trazem desafios de qualidade.
* **An Empirical Evaluation... Technical Debt and Software Security:** Relacionou dívida técnica com falhas de segurança.
* **Impact of Continuous Integration... (Bhattacharya):** Evidenciou que CI aumenta a qualidade ao detectar erros cedo.

### 2.4 Referencial teórico e empírico essencial
* **Rapid Release (RR):** Projetos com mediana de tempo entre releases inferior a 35 dias.
* **Slow Release (SR):** Projetos com mediana de tempo entre releases igual ou superior a 50 dias.
* **Aspectos de Qualidade:** O estudo fundamenta-se na análise de três pilares: vulnerabilidades, erros (bugs e *code smells*) e retrabalho (dívida técnica).

---

## 3. Objetivos e questões (Goal / Question / Metric)

### 3.1 Objetivo geral (Goal template)
**Analisar** estratégias de lançamento (*rapid* vs. *slow release*) **com o propósito de** comparar suas influências na qualidade do código **com respeito a** vulnerabilidades, erros e retrabalho **do ponto de vista de** gerentes de projeto **no contexto de** repositórios *open-source*.

### 3.2 Objetivos específicos
* Fornecer uma visão organizada dos impactos de cada estratégia para auxiliar na tomada de decisão.
* Verificar se a dívida técnica e a densidade de código duplicado variam conforme a estratégia de release.
* Comparar a frequência de bugs e *code smells* entre os dois grupos de repositórios.

### 3.3 Questões de pesquisa / de negócio
* **RQ1:** O RRC (*Rapid Release Cycle*) torna as releases mais vulneráveis?
* **RQ2:** Erros são mais comuns em releases de RRC?
* **RQ3:** O retrabalho é maior em sistemas que utilizam RRC, do que em sistemas que utilizam releases lentas?

### 3.4 Métricas associadas (GQM)

| Questão Associada | Métrica (SonarQube) | Definição/Contexto | Fonte de Dados |
| :--- | :--- | :--- | :--- |
| **RQ1 (Segurança)** | `vulnerabilities` | Quantidade absoluta de vulnerabilidades de segurança. | SonarQube |
| **RQ1 (Segurança)** | `security_rating` | Nota de segurança baseada na severidade das vulnerabilidades (1=Melhor, 5=Pior). | SonarQube |
| **RQ2 (Erros)** | `bugs` | Quantidade de bugs detectados estaticamente. | SonarQube |
| **RQ2 (Erros)** | `code_smells` | Quantidade de "maus cheiros" de código que indicam problemas de design. | SonarQube |
| **RQ2 (Erros)** | `reliability_rating` | Nota de confiabilidade (1=Melhor, 5=Pior). | SonarQube |
| **RQ3 (Retrabalho)** | `sqale_index` | Índice de Dívida Técnica (esforço estimado para corrigir problemas). | SonarQube |
| **RQ3 (Retrabalho)** | `duplicated_lines_density` | Densidade (%) de linhas de código duplicadas. | SonarQube |
| **RQ3 (Retrabalho)** | `sqale_rating` | Nota de manutenibilidade baseada no índice SQALE. | SonarQube |
| **Geral** | `ncloc` | Linhas de código não comentadas (para dimensionamento). | SonarQube |
