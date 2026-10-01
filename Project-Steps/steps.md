# OpsReady

**Alunos:**<br>
Carlos Eduardo Araujo<br>
Maria Eduarda de Abreu Cordeiro<br>
Gabriel Lucas Izidorio Costa<br>
Arthur Takenaka do Carmo<br>

---

### _ETAPA 1_

1. **Quem é o usuário?**
   - **Analistas de suporte/CoE:** Profissionais técnicos que recebem demandas já triadas, contextualizadas e categorizadas pelo sistema.
   - **Usuários finais (colaboradores de outras áreas da empresa):** Qualquer funcionário da organização (ex.: Vendas, RH, Financeiro) que precisa de suporte técnico, tirar dúvidas sobre processos internos ou consultar dados operacionais aos quais tem permissão, onde terá como escolher usar o agent dentro da aplicação, sem precisar navegar por interfaces complexas ou preencher formulários extensos.
   - **Administrador do Sistema / Gestor de Atendimento:** Responsável por cadastrar as regras de negócio, gerenciar os acessos dos colaboradores e acompanhar métricas básicas de volume e resolução de chamados.

2. **Qual problema nosso projeto resolve?**

   O projeto soluciona gargalos operacionais críticos no fluxo de suporte tradicional, como:
   - **Sobrecarga no Suporte N1 com Triagem Manual:** Analistas perdem horas reclassificando chamados mal preenchidos ou respondendo dúvidas simples e repetitivas antes de conseguir direcionar os incidentes para os especialistas corretos.
   - **Falta de Transparência e Risco de Erro por "Caixa Preta":** Soluções de automação total frequentemente erram o contexto do usuário por falta de revisão humana. O projeto resolve isso inserindo uma etapa de revisão visual imediata (Human-in-the-Loop).
   - **Dificuldade de Acesso Seguro a Informações Corporativas:** Usuários gastam tempo procurando dados operacionais espalhados em sistemas legados, quando poderiam obter respostas diretas via chat respeitando suas permissões individuais de acesso.

3. **Quem são os interessados?**
   - **Usuários de Negócio / Colaboradores Operacionais (ex.: Vendedor do CRM, Assistente Fiscal):** Interessados na agilidade de atendimento, em um processo sem burocracia para relatar incidentes e em obter respostas rápidas sem interromper seu fluxo de trabalho.
   - **Liderança de TI / CoE (Centro de Excelência):** Interessados na otimização da equipe técnica, redução de custos operacionais e padronização da qualidade dos dados que entram na fila de atendimento.
   - **Equipe de Governança e Segurança da Informação:** Interessados na garantia de que o agente conversacional consulte apenas dados permitidos para o perfil de cada colaborador (RBAC) e que os chamados criados mantenham rastreabilidade e integridade.

4. **Por que seu projeto gera valor?**
   - **Abertura Inteligente com Revisão Humana (Human-in-the-Loop):** O usuário apenas relata o problema em texto livre; o agente (via API do Gemini) interpreta o contexto, extrai os dados e monta automaticamente o formulário do chamado na tela. O usuário revisa, faz ajustes se necessário e confirma o envio, unindo velocidade à precisão das informações.
   - **Triagem e Roteamento Automático N1:** O agente classifica o incidente e já define a prioridade e o setor de destino correto (ex.: Infraestrutura, ERP, Telecom), liberando o time técnico de N1 de tarefas repetitivas de triagem.
   - **Autoconsumo Seguro de Informação:** Colaboradores realizam consultas operacionais diretas no chat com segurança garantida na camada de API (a IA só acessa o que o token de autenticação do usuário permite).

---

### _ETAPA 2_

### 1. **Personas**

**Persona Principal: Lucas Silva (Usuário Final / Solicitante)**

- **Cargo:** Assistente de Vendas / Setor Operacional.
- **Idade:** 28 anos.
- **Perfil Técnico:** Baixo a médio. Utiliza ferramentas cotidianas (CRM, e-mail, planilhas), mas não domina termos técnicos de infraestrutura ou governança de TI.
- **Dores:** Perde tempo tentando identificar categorias e subcategorias em formulários convencionais; acha os sistemas de chamados burocráticos e complexos; tem dificuldade para acompanhar o andamento de suas solicitações.
- **Objetivo:** Relatar problemas em linguagem natural, obter respostas rápidas e ter seu chamado aberto com agilidade para não interromper seu fluxo de trabalho.

### Persona Secundária: Mariana Costa (Analista de Suporte N2)

- **Cargo:** Analista de Sistemas / Suporte Técnico N2.
- **Idade:** 34 anos.
- **Perfil Técnico:** Alto.
- **Dores:** Recebe frequentemente chamados mal descritos ("o sistema não funciona"), com prioridades arbitrárias ou atribuídos para a fila errada, gastando tempo operacional com triagem manual.
- **Objetivo:** Receber chamados já padronizados, com contexto técnico estruturado, prioridade coerente e resumo objetivo para focar diretamente no diagnóstico e resolução.

### 2. **Jornada do Usuário**

**Cenário:** Lucas tenta extrair um relatório de fechamento no sistema corporativo e recebe um erro de permissão.

1. **Identificação da Necessidade:** Lucas acessa a aplicação web e abre a interface de chat com o agente.
2. **Entrada em Linguagem Natural:** Lucas envia: _"Estou tentando gerar o relatório de vendas de agosto, mas o sistema diz que não tenho permissão."_
3. **Processamento do Agente (Gemini):** O backend consome a API do Gemini com saída estruturada (JSON), identifica a intenção (permissão/acesso), extrai os detalhes técnicos, classifica o incidente para a fila de sistemas e infere a urgência.
4. **Geração e Revisão do Formulário (_Human-in-the-Loop_):** O frontend recebe os dados estruturados e apresenta na tela um formulário de chamado totalmente pré-preenchido (título, categoria, urgência, setor de destino e descrição).
5. **Validação do Solicitante:** Lucas confere os dados sugeridos pela IA, ajusta algum detalhe se necessário e clica em **"Confirmar e Criar Chamado"**.
6. **Efetivação e Encaminhamento:** O backend persiste o chamado no banco de dados, vincula o ticket diretamente à fila de atendimento da equipe da Mariana (N2) e disponibiliza o código de protocolo para Lucas acompanhar.

### 3. **Requisitos Funcionais e Não Funcionais**

**Requisitos Funcionais (RF)**

- **RF01 - Autenticação e Autorização:** O sistema deve autenticar usuários e controlar acessos por meio de tokens JWT, identificando o papel de cada usuário.
- **RF02 - Interface Conversacional com Agente:** O sistema deve fornecer uma interface de chat para envio de mensagens em linguagem natural processadas via API do Gemini.
- **RF03 - Geração Assistida de Formulário:** O sistema deve converter o relato livre do usuário em um rascunho de chamado com campos técnicos estruturados (JSON).
- **RF04 - Revisão de Chamado (_Human-in-the-Loop_):** O sistema deve permitir ao usuário visualizar, editar e aprovar os dados do formulário sugerido antes de confirmar a persistência.
- **RF05 - Persistência e Roteamento de Tickets:** O sistema deve registrar o chamado confirmado no banco de dados e direcioná-lo automaticamente à fila N2 indicada na triagem.
- **RF06 - Consulta de Informações via Chat:** O sistema deve responder a dúvidas e consultas de chamados via chat, respeitando as restrições de permissão do usuário logado.
- **RF07 - Visualização da Fila N2:** O sistema deve fornecer aos analistas uma listagem dos chamados de sua área com opção de atualização de status (ex.: _Em Andamento_, _Resolvido_).

**Requisitos Não Funcionais (RNF)**

- **RNF01 - Arquitetura de Comunicação:** Toda a integração entre frontend e backend deve ocorrer exclusivamente por meio de endpoints HTTP REST padronizados em JSON.
- **RNF02 - Validação Estruturada da IA:** As requisições ao Gemini devem utilizar esquema de resposta estrito (`response_schema`), assegurando retorno consistente em JSON para o backend.
- **RNF03 - Controle de Acesso Baseado em Papéis (RBAC):** Consultas a dados sensíveis realizadas via agente devem ser validadas pela API antes da execução de qualquer leitura no banco.
- **RNF04 - Tempo Máximo de Resposta:** O processamento da IA para estruturação do formulário de chamado não deve ultrapassar 5 segundos.
- **RNF05 - Usabilidade e Eficiência:** A abertura completa do chamado, da mensagem inicial à confirmação final, deve exigir no máximo 3 cliques de navegação.

### 4. **Modelagem de Casos de Uso**

**Atores**

- **Usuário Final:** Colaborador que interage via chat, valida formulários de chamados e realiza consultas.
- **Analista N2:** Técnico que gerencia a fila de atendimento da sua especialidade e atualiza os status dos tickets.
- **Serviço de IA (Gemini API):** Componente externo responsável pelo processamento de linguagem natural e estruturação de dados.

### Casos de Uso

| Identificador | Nome do Caso de Uso        | Atores Principais          | Descrição Sumária                                                                         |
| :------------ | :------------------------- | :------------------------- | :---------------------------------------------------------------------------------------- |
| **UC01**      | Autenticar no Sistema      | Usuário Final, Analista N2 | Realiza login informando credenciais e obtém token JWT.                                   |
| **UC02**      | Interagir com o Agente     | Usuário Final, Gemini API  | Envia relato livre de problema ou dúvida operacional via chat.                            |
| **UC03**      | Gerar Rascunho de Chamado  | Usuário Final, Gemini API  | Estrutura os dados da conversa em JSON e exibe o formulário pré-preenchido.               |
| **UC04**      | Confirmar e Criar Chamado  | Usuário Final              | Revisa os campos do formulário, ajusta dados se necessário e grava o ticket no banco.     |
| **UC05**      | Consultar Dados via Chat   | Usuário Final, Gemini API  | Solicita informações sobre suas demandas; a API valida a autorização e exibe o resultado. |
| **UC06**      | Atender Chamado na Fila N2 | Analista N2                | Consulta tickets atribuídos à sua equipe e atualiza o status de atendimento.              |
