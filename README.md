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

Com certeza. Aqui está o Plano de Experimento reestruturado com base no PDF, sem as citações:

#### 4. Escopo e contexto do experimento
* **4.1 Escopo funcional:** Mineração de dados de repositórios públicos e análise estática de código. Exclui projetos que não atendem aos critérios de popularidade e atividade definidos.
* **4.2 Contexto do estudo:** 1400 repositórios do GitHub (top stars), abrangendo diversos domínios, analisados via automação.
* **4.3 Premissas:** Assume-se que as métricas do SonarQube são indicadores válidos de qualidade e segurança e que a mediana de tempo de release reflete a estratégia do projeto.
* **4.4 Restrições:** Limitações da API do GitHub e capacidade de processamento para clonar/analisar 1400 repositórios.
* **4.5 Limitações previstas:** A análise é puramente estática e baseada em dados históricos; não avalia a funcionalidade dinâmica ou a satisfação do usuário final.

#### 5. Stakeholders e impacto esperado
* **5.1 Stakeholders principais:** Gerentes de projeto de software, engenheiros de release e pesquisadores da área.
* **5.2 Interesses e expectativas:** Obter uma visão organizada dos impactos das estratégias para fundamentar decisões sobre o ciclo de lançamentos.
* **5.3 Impactos potenciais:** Fornecer evidências de que *rapid releases* podem exigir maior rigor de qualidade para evitar acúmulo de bugs e dívida técnica.

#### 6. Riscos de alto nível, premissas e critérios de sucesso
* **6.1 Riscos de alto nível:** Falha na mineração dos dados (mudanças na API), inconclusividade estatística entre os grupos, ou dados "ruidosos" em repositórios open-source.
* **6.2 Critérios de sucesso globais:** Capacidade de classificar os repositórios em RR e SR e obter diferenças estatísticas observáveis nas métricas de qualidade.
* **6.3 Critérios de parada antecipada:** Incapacidade de coletar um dataset significativo (mínimo definido de repositórios válidos) que atenda aos filtros.

#### 7. Modelo conceitual e hipóteses
* **7.1 Modelo conceitual:** O tempo entre releases (variável independente) influencia a acumulação de defeitos e vulnerabilidades (variáveis dependentes) devido à pressão de tempo ou frequência de feedback.
* **7.2 Hipóteses formais:**
    * **H1,1 (Alternativa):** Projetos RR são significativamente mais vulneráveis que projetos SR.
    * **H1,2 (Alternativa):** Erros são significativamente mais comuns em projetos RR que em SR.
    * **H1,3 (Alternativa):** O retrabalho é significativamente maior em projetos RR que em SR.
* **7.3 Nível de significância:** O estudo busca identificar "diferença significativa", implicitamente seguindo padrões acadêmicos (geralmente p < 0.05).

#### 8. Variáveis, fatores, tratamentos e objetos de estudo
* **8.1 Objetos de estudo:** Repositórios de código fonte no GitHub.
* **8.2 Sujeitos / participantes:** Não se aplica (estudo de artefatos de software).
* **8.3 Variáveis independentes:** Tipo de Ciclo de Release.
* **8.4 Tratamentos:**
    * *Grupo 1 (Rapid Release - RR):* Mediana de releases entre 5 e 35 dias.
    * *Grupo 2 (Slow Release - SR):* Mediana de releases $\geq$ 50 dias.
* **8.5 Variáveis dependentes:** Métricas de Vulnerabilidades, Bugs, Code Smells e Dívida Técnica.
* **8.6 Variáveis de controle / bloqueio:** Filtros de popularidade (stars) e atividade (forks, colaboradores) para garantir relevância dos projetos.

#### 9. Desenho experimental
* **9.1 Tipo de desenho:** Estudo Observacional Comparativo (Ex-post facto), baseado em Mineração de Repositórios de Software (MSR).
* **9.2 Randomização e alocação:** Não há randomização de tratamento (os projetos já escolheram suas estratégias). A seleção é baseada em critérios pré-definidos aplicados a um ranking.
* **9.3 Balanceamento:** O estudo busca os "top" repositórios e depois filtra, resultando em grupos formados naturalmente pelos dados minerados.
* **9.4 Número de grupos:** Dois grupos principais de comparação (Rapid vs. Slow).

#### 10. População, sujeitos e amostragem
* **10.1 População-alvo:** Projetos de software Open Source relevantes.
* **10.2 Critérios de inclusão:** Top 1400 repositórios por *stars*, 50+ forks, 50+ stars, mínimo de 19 colaboradores e 19 releases.
* **10.3 Critérios de exclusão:** Repositórios que não se encaixam nas janelas de mediana de release definidas ou que não possuem dados suficientes.
* **10.4 Tamanho da amostra planejado:** Mineração inicial de 5000 repositórios para filtrar os top 1400 elegíveis.
* **10.5 Método de seleção:** Amostragem intencional baseada em ranking de popularidade (stars).
* **10.6 Treinamento:** Não aplicável.

#### 11. Instrumentação e protocolo operacional
* **11.1 Instrumentos de coleta:** Script em Python para mineração (GitHub GraphQL API) e Ferramenta SonarQube para análise estática.
* **11.2 Materiais de suporte:** Documentação da API do GitHub e manuais de métricas do SonarQube.
* **11.3 Procedimento experimental:**
    1.  Minerar top 1400 repositórios via API.
    2.  Filtrar dados e classificar em RR ou SR.
    3.  Clonar repositórios (Git).
    4.  Executar análise do SonarQube.
    5.  Salvar métricas em CSV e analisar estatisticamente.
* **11.4 Plano de piloto:** Teste inicial dos scripts de mineração para validar a coleta dos dados JSON.

#### 12. Plano de análise de dados
* **12.1 Estratégia geral:** Comparar as distribuições das métricas de qualidade entre os grupos RR e SR para validar ou refutar as hipóteses.
* **12.2 Métodos estatísticos planejados:** Cálculo de medianas, uso de Boxplots para visualização de distribuição e dispersão (quartis).
* **12.3 Tratamento de dados faltantes:** Repositórios sem dados suficientes de releases ou colaboradores são filtrados antes da análise.
* **12.4 Análise qualitativa:** Interpretação dos resultados à luz da literatura de Engenharia de Release.

#### 13. Avaliação de validade
* **13.1 Validade de conclusão:** Garantida pelo tamanho da amostra (1400 repositórios) e uso de métricas padronizadas.
* **13.2 Validade interna:** Controle de variáveis de confusão através de critérios rígidos de inclusão (tamanho do projeto, número de colaboradores).
* **13.3 Validade de constructo:** Uso de ferramenta de mercado (SonarQube) amplamente aceita para mensurar "Qualidade" e "Dívida Técnica".
* **13.4 Validade externa:** Resultados focados em Open Source; generalização para ambientes industriais fechados deve ser feita com cautela.

#### 14. Ética, privacidade e conformidade
* **14.1 Questões éticas:** Uso de dados públicos de repositórios Open Source.
* **14.2 Consentimento:** Não necessário (dados públicos).
* **14.3 Privacidade:** O estudo foca em métricas de código, não em dados pessoais sensíveis dos desenvolvedores.
* **14.4 Aprovações:** Aprovação acadêmica do departamento da PUC-Minas.

#### 15. Recursos, infraestrutura e orçamento
* **15.1 Recursos humanos:** 4 pesquisadores/autores.
* **15.2 Infraestrutura técnica:** Máquinas para execução de scripts Python, armazenamento de JSON/CSV, ambiente com Git e servidor SonarQube instalado.
* **15.3 Materiais:** Acesso à Internet e Tokens de API do GitHub.
* **15.4 Orçamento:** Custos operacionais de pesquisa acadêmica (infraestrutura computacional e horas de pesquisa).

#### 16. Cronograma, marcos e riscos operacionais
* **16.1 Marcos:** 1. Desenvolvimento do Script de Mineração; 2. Coleta e Filtragem (Dataset JSON); 3. Análise SonarQube (Processamento em lote); 4. Redação do Artigo.
* **16.2 Dependências:** A análise (SonarQube) depende da conclusão e limpeza da mineração de dados.
* **16.3 Riscos operacionais:** Bloqueio da API do GitHub (Rate Limit) ou falhas na clonagem de repositórios grandes.

#### 17. Governança do experimento
* **17.1 Papéis:** Autores conduzem a execução e análise; Orientadores/Revisores validam a metodologia.
* **17.2 Ritos:** Reuniões de acompanhamento do grupo de pesquisa.
* **17.3 Controle de mudanças:** Ajustes nos filtros de seleção (ex: número de stars) documentados no script de filtragem.

#### 18. Plano de documentação e reprodutibilidade
* **18.1 Repositórios:** Scripts e Datasets salvos em formatos JSON e CSV.
* **18.2 Artefatos padrão:** Scripts Python para mineração e análise automatizada.
* **18.3 Empacotamento:** O estudo visa complementar a literatura existente, sugerindo a disponibilização dos dados gerados.

#### 19. Plano de comunicação
* **19.1 Públicos:** Comunidade acadêmica e gestores de projeto.
* **19.2 Canais:** Publicação de artigo científico.
* **19.3 Mensagem chave:** Rapid releases exigem maior atenção à qualidade para evitar degradação do código.

#### 20. Critérios de prontidão para execução
* **20.1 Checklist:** Scripts de mineração testados? Ambiente SonarQube configurado? Critérios de filtro (RR vs SR) definidos?
* **20.2 Aprovação final:** Validação da metodologia pelos autores antes do início da mineração em larga escala.
