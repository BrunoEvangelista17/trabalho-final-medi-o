# Definição de Experimento: Análise de Estratégias de Release e Qualidade de Código

## 1. Identificação básica

### 1.1 Título do experimento
Análise Comparativa de Repositórios com Releases Rápidos e Lentos: Implicações para a Qualidade do Código.

### 1.2 Autores (nome, área, contato)
* **Alfredo L. Vieira** (Departamento de Engenharia de Software e Sistemas da Informação - PUC-Minas).
* **Bruno E. Gomes de Azevedo** (Departamento de Engenharia de Software e Sistemas da Informação - PUC-Minas).
* **Estevão de F. Rodrigues** (Departamento de Engenharia de Software e Sistemas da Informação - PUC-Minas).
* **Vinícius S. de Oliveira** (Departamento de Engenharia de Software e Sistemas da Informação - PUC-Minas).

### 1.3 Projeto / produto / iniciativa relacionada
Pesquisa acadêmica sobre Engenharia de Software, focada em estratégias de *release* (lançamento) e qualidade de software em projetos *open-source*.

---

## 2. Contexto e problema

### 2.1 Descrição do problema / oportunidade
Gerentes de projeto frequentemente enfrentam dúvidas sobre qual estratégia de lançamento adotar, precisando avaliar os *tradeoffs* entre estratégias de lançamento rápido (*rapid release*) e lento (*slow release*). Uma decisão equivocada pode levar a custos elevados de manutenção, insatisfação e perda de competitividade. O estudo busca esclarecer como essas estratégias impactam a qualidade final do produto.

### 2.2 Contexto organizacional e técnico
* **Ambiente:** Projetos *open-source* hospedados no GitHub.
* **Amostra:** 2000 repositórios minerados (Top stars, >50 forks, >19 colaboradores).
* **Tecnologias/Ferramentas:** API GraphQL do GitHub para mineração, scripts em Python para automação e filtragem, e SonarQube para análise estática de código.

### 2.3 Trabalhos e evidências prévias (internos e externos)
* **RapidRelease - A Dataset of Projects... (Joshi & Chimalakonda, 2019):** Forneceu a definição de *rapid release* (ciclo médio entre 5 e 35 dias) e o dataset base.
* **Modern Release Engineering in a Nutshell:** Base para entendimento das fases do pipeline de engenharia de release.
* **Systematic literature review on... Agile Release Engineering:** Indicou que releases rápidas melhoram eficiência, mas trazem desafios de qualidade.
* **An Empirical Evaluation... Technical Debt and Software Security:** Relacionou dívida técnica com falhas de segurança.
* **Impact of Continuous Integration... (Bhattacharya):** Evidenciou que CI aumenta a qualidade ao detectar erros cedo.

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

---

## 4. Escopo e contexto do experimento

### 4.1 Escopo funcional / de processo
* **Incluído:** Mineração de dados em massa via API do GitHub, clonagem de repositórios e análise estática de código automatizada utilizando a ferramenta SonarQube.
* **Excluído:** Repositórios que não atendem aos critérios mínimos de popularidade e atividade (número de stars, forks e colaboradores) definidos nos filtros.

### 4.2 Contexto do estudo
* **Organização:** Pesquisa acadêmica (PUC-Minas) focada em dados públicos.
* **Alvo:** Projetos *open-source* hospedados na plataforma GitHub.
* **Tipo de Análise:** Estudo observacional (*ex-post facto*) baseado no histórico de *releases* e na qualidade atual do código.

### 4.3 Premissas
* A mediana do tempo entre *releases* é um indicador válido para categorizar a estratégia de desenvolvimento de um projeto (Rápida vs. Lenta).
* As métricas fornecidas pelo SonarQube (como *Security Rating* e *Reliability Rating*) são indicadores confiáveis da qualidade real do software.

### 4.4 Restrições
* Dependência da disponibilidade e dos limites de taxa (*rate limits*) da API GraphQL do GitHub.
* Capacidade computacional para clonar e processar a análise estática de 1.400 repositórios.

### 4.5 Limitações previstas
* O estudo baseia-se puramente em análise estática; não são realizados testes dinâmicos ou funcionais.
* Os resultados refletem o contexto de projetos *open-source*, podendo não ser totalmente generalizáveis para ambientes corporativos fechados com processos diferentes.

---

## 5. Stakeholders e impacto esperado

### 5.1 Stakeholders principais
* Gerentes de projeto de software.
* Engenheiros de software e equipes de DevOps.
* Pesquisadores acadêmicos na área de Engenharia de Software.

### 5.2 Interesses e expectativas dos stakeholders
* **Gerentes:** Necessitam de dados para apoiar a decisão sobre qual estratégia de *release* adotar, compreendendo os riscos de cada uma.
* **Pesquisadores:** Buscam evidências empíricas que relacionem práticas de engenharia de *release* com a qualidade do produto final.

### 5.3 Impactos potenciais no processo / produto
* Evidenciar que a escolha da estratégia de *release* impacta diretamente custos de manutenção e segurança.
* Incentivar a adoção de práticas de qualidade mais rigorosas em projetos que optam por ciclos rápidos (*rapid releases*).

---

## 6. Riscos de alto nível, premissas e critérios de sucesso

### 6.1 Riscos de alto nível
* Inconsistência nos dados minerados do GitHub (ex: repositórios apagados ou metadados incompletos).
* Saber diferênciar uma release completa de hotfix ou outras mudanças menores
* Dificuldade de encontrar repositórios de Slow Release

### 6.2 Critérios de sucesso globais
* Consegui processar uma amostra significativa.
* Identificar diferenças estatísticas ou tendências claras entre os grupos RR e SR nas métricas de qualidade.

### 6.3 Critérios de parada antecipada
* Não ter repositórios suficientes para a análise de Rapid e Slow release. (2000 repositórios -> 1400 repositórios)

---

## 7. Modelo conceitual e hipóteses

### 7.1 Modelo conceitual do experimento
A frequência de lançamentos (variável independente) influencia a qualidade interna do código (variável dependente), afetando a probabilidade de inserção de vulnerabilidades, a densidade de bugs e o acúmulo de dívida técnica.

### 7.2 Hipóteses formais
* **Vulnerabilidade (H1):**
    * $H_{0,1}$: Não há diferença significativa na vulnerabilidade entre projetos de Release Rápida (RRC) e Release Lenta (SL).
    * $H_{1,1}$: Projetos RRC são significativamente mais vulneráveis que projetos SL.
* **Erros (H2):**
    * $H_{0,2}$: Não há diferença significativa na ocorrência de erros entre RRC e SL.
    * $H_{1,2}$: Erros são significativamente mais comuns em projetos RRC que em SL.
* **Retrabalho (H3):**
    * $H_{0,3}$: Não há diferença significativa no retrabalho (Dívida Técnica) entre RRC e SL.
    * $H_{1,3}$: O retrabalho é significativamente maior em projetos RRC que em SL.

### 7.3 Nível de significância e considerações de poder
* O estudo busca validar se as diferenças de médias/medianas entre os grupos são "significativas", utilizando métricas estatísticas descritivas (boxplot, mediana) para suportar as conclusões.

---

## 8. Variáveis, fatores, tratamentos e objetos de estudo

### 8.1 Objetos de estudo
* Repositórios de código-fonte minerados do GitHub.

### 8.2 Sujeitos / participantes
* Não aplicável (estudo de artefatos de software).

### 8.3 Variáveis independentes (fatores)
* **Tipo de Ciclo de Release:** Variável categórica binária (Rapid Release vs. Slow Release).

### 8.4 Tratamentos (condições experimentais)
* **Grupo RR (Rapid Release):** Mediana de tempo entre releases entre 5 e 35 dias.
* **Grupo SR (Slow Release):** Mediana de tempo entre releases de 50 dias ou mais.

### 8.5 Variáveis dependentes (respostas)
* **Métricas de Segurança:** Vulnerabilidades, *Security Rating*.
* **Métricas de Confiabilidade:** Bugs, *Reliability Rating*, *Code Smells*.
* **Métricas de Manutenibilidade:** *Sqale Index* (Dívida Técnica), Densidade de Linhas Duplicadas, *Sqale Rating*.

### 8.6 Variáveis de controle / bloqueio
* Popularidade (*Stars*).
* Tamanho da comunidade (Colaboradores, *Forks*).
* Maturidade do projeto (Número mínimo de *releases*).

---

## 9. Desenho experimental

### 9.1 Tipo de desenho
Estudo empírico de Mineração de Repositórios de Software (MSR), comparativo e quantitativo.

### 9.2 Randomização e alocação
Seleção baseada em ranking (Top Stars) com alocação nos grupos de tratamento determinada pelas características históricas do próprio repositório (data das *releases*).

### 9.3 Balanceamento
Os grupos são formados após a filtragem dos 15.000 repositórios iniciais, resultando nos 1.400 mais relevantes divididos conforme sua cadência.

### 9.4 Número de grupos
Dois grupos de comparação: Rápido e Lento.

---

## 10. População, sujeitos e amostragem

### 10.1 População-alvo
Projetos de software *open-source* ativos e relevantes na comunidade global.

### 10.2 Critérios de inclusão de sujeitos
* Estar entre os top 1400 repositórios em número de *stars*.
* Possuir mais de 50 *forks*.
* Possuir mais de 50 *stars*.
* Possuir no mínimo 19 colaboradores e histórico de *releases*.

### 10.3 Critérios de exclusão de sujeitos
* Projetos com métricas de release inconclusivas ou que caem no intervalo entre 35 e 50 dias (zona cinzenta não analisada).

### 10.4 Tamanho da amostra planejado
* Mineração inicial: 15.000 repositórios. 
* Amostra final processada: 1.400 repositórios.

### 10.5 Método de seleção / recrutamento
Automação via scripts Python utilizando a API do GitHub.

---

## 11. Instrumentação e protocolo operacional

### 11.1 Instrumentos de coleta
* **Python Scripts:** Para consulta à API GraphQL do GitHub e filtragem dos dados JSON.
* **Git:** Ferramenta de versionamento para clonar os códigos.
* **SonarQube:** Ferramenta de análise estática para gerar as métricas de qualidade.

### 11.2 Materiais de suporte
* Dataset de referência "RapidRelease" (Joshi and Chimalakonda).

### 11.3 Procedimento experimental (Protocolo passo a passo)
1.  **Obter dados:** Consumir API do GitHub para buscar os top 5000 repositórios.
2.  **Filtrar:** Aplicar critérios de inclusão e calcular medianas de release para classificar os projetos.
3.  **Salvar Dataset:** Gerar arquivo JSON com os repositórios selecionados.
4.  **Preparação:** Configurar ambiente de análise.
5.  **Processamento:** Iterar sobre o JSON, clonar cada repositório e executar o *scanner* do SonarQube.
6.  **Exportação:** Salvar os resultados das métricas em formato .CSV para análise.

---

## 12. Plano de análise de dados

### 12.1 Estratégia geral de análise
Análise comparativa direta entre as medianas e distribuições das métricas dos dois grupos (RR e SR).

### 12.2 Métodos estatísticos planejados
* Cálculo de medianas para métricas absolutas (bugs, code smells, dívida técnica).
* Visualização através de Boxplots para entender a dispersão (quartis).
* Comparação percentual de *Ratings* (escalas de 1 a 5).

### 12.3 Tratamento de dados faltantes e outliers
* A visualização dos dados foca nos "95% inferiores", indicando tratamento para remover o ruído de *outliers* extremos que poderiam distorcer a análise.

---

## 13. Avaliação de validade

### 13.1 Validade de conclusão
Assegurada pelo volume da amostra (1.400 projetos), permitindo inferências estatísticas sobre o comportamento dos grupos.

### 13.2 Validade interna
Mitigada pelo uso de critérios rigorosos de seleção (tamanho e atividade do projeto) para garantir que estamos comparando projetos de relevância similar.

### 13.3 Validade de constructo
Uso de ferramenta padrão de mercado (SonarQube) cujas métricas (como SQALE Index) são amplamente aceitas como *proxies* para qualidade técnica.

### 13.4 Validade externa
Os resultados são válidos para o ecossistema *open-source*; a generalização para contextos industriais privados deve considerar as diferenças nos processos de desenvolvimento.

---

## 14. Ética, privacidade e conformidade

### 14.1 Questões éticas
O estudo utiliza apenas dados públicos de repositórios de código, sem envolver experimentação direta com seres humanos ou dados sensíveis.

### 14.3 Privacidade e proteção de dados
Os dados coletados referem-se a métricas de código e metadados públicos de projetos, respeitando os termos de uso da plataforma GitHub.

---

## 15. Recursos, infraestrutura e orçamento

### 15.1 Recursos humanos
Equipe de quatro pesquisadores/autores.

### 15.2 Infraestrutura técnica necessária
* Acesso à internet e chaves de API do GitHub.
* Máquinas para execução dos scripts de mineração e do servidor SonarQube.
* Ferramentas de BI para visualização dos dados.

### 15.3 Materiais e insumos
* Base de conhecimento acadêmica sobre Engenharia de Release.

---

## 16. Cronograma, marcos e riscos operacionais

### 16.1 Marcos principais
1.  Desenvolvimento dos scripts de mineração.
2.  Coleta e filtragem dos dados (Geração do JSON).
3.  Execução da análise estática (SonarQube).
4.  Consolidação dos dados em CSV e análise dos resultados.
5.  Redação final do artigo.

---

## 17. Governança do experimento

### 17.1 Papéis e responsabilidades
Os autores do estudo dividem as tarefas de implementação dos scripts, execução da análise e interpretação dos dados estatísticos.

---

## 18. Plano de documentação e reprodutibilidade

### 18.1 Repositórios e convenções
Armazenamento dos dados brutos em JSON e dados processados em CSV.

Aqui está a **versão simplificada**, consolidada em **uma única seção**, com menos itens e mantendo apenas o essencial:

---

## **18.2 Templates e artefatos padrão**

O experimento utiliza um conjunto reduzido e padronizado de artefatos para garantir reprodutibilidade e consistência dos processos. Os principais são:

### **1. Checklists e modelos**

* **Checklist de Preparação do Ambiente:** valida instalação e configuração de Python, Git e SonarQube.
* **Template de Validação dos Dados:** usado para verificar integridade dos CSVs gerados.

---

### **2. Scripts principais**

* **Coleta e Mineração (`miner_github.py`)** – consulta a API e aplica filtros.
* **Classificação das Releases (`process_releases.py`)** – calcula medianas e define RR ou SR.
* **Clonagem e Análise (`clone_and_scan.py`)** – clona repositórios e executa o SonarQube.
* **Exportação de Métricas (`export_metrics.py`)** – gera arquivos CSV finais.
* 
---

### **3. Artefatos de dados**

* **Dataset JSON com repositórios filtrados**
* **CSV final das métricas de qualidade**
* **Template padrão do SonarQube (`sonar-project.properties`)**

### 18.3 Plano de empacotamento
A metodologia é descrita detalhadamente (parâmetros de filtro, ferramentas usadas) para permitir que outros pesquisadores repliquem a mineração e análise.

---

## 19. Plano de comunicação

### 19.1 Públicos e mensagens-chave
O estudo visa comunicar à comunidade de engenharia de software que tende a cada vez mais agilizar os ciclos de desenvolvimento, mostrando qual que é o verdadeiro efeito que o tempo de desenvolvimento tem sobre o código.

### 19.2 Canais
Publicação de artigo em conferência/periódico acadêmico.

---

### 20. Metodologia

[![metodologia](https://github.com/BrunoEvangelista17/trabalho-final-medi-o/blob/main/image.png)](https://github.com/BrunoEvangelista17/trabalho-final-medi-o/blob/main/image.png)
