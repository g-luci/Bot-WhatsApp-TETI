# OpsReady

**Alunos:**<br> 
Carlos Eduardo Araujo<br>
Maria Eduarda de Abreu Cordeiro<br>
Gabriel Lucas Izidorio Costa<br>
Arthur Takenaka do Carmo<br>

---

### *ETAPA 1*

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