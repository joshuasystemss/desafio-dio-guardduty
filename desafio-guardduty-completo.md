# Do Alerta à Resposta: Prompt para Investigar um Achado do Amazon GuardDuty

Este arquivo reúne as respostas dos três passos e o prompt final (Passo 3), pronto para copiar e colar.

---

## Passo 1: Descreva o Achado e Quem Vai Ler a Sua Análise

```text
Você é um analista de segurança em nuvem especializado em AWS e vai me ajudar a investigar um achado do Amazon GuardDuty.

1. Descrição do achado
- Tipo: UnauthorizedAccess:EC2/SSHBruteForce
- Recurso afetado: instância EC2 em sub-rede pública, que hospeda o painel administrativo de testes de uma loja virtual
- Severidade: 2.0, baixa
- Quando: entre 01h30 e 02h50 de uma quarta-feira, horário de Brasília
- O que o GuardDuty descreve: tentativas repetidas de autenticação SSH na porta 22, partindo de um único endereço IP externo, durante cerca de oitenta minutos

2. Público-alvo
- Quem vai ler a análise: profissional de infraestrutura responsável pelo monitoramento da AWS, com bom conhecimento de Linux e conhecimento básico de segurança em nuvem.
- O que eu preciso ao final: decidir se bloqueio o acesso SSH à instância agora ou se continuo investigando antes de agir.
```

---

## Passo 2: Contexto do Ambiente, Formato da Resposta e Limites

```text
3. Contexto do ambiente, até onde consigo confirmar hoje
- A instância hospeda o painel de testes. Se sair do ar, o time de desenvolvimento perde o ambiente por algumas horas, mas nenhum cliente é afetado.
- Quem acessa: apenas o time de desenvolvimento (5 pessoas), por SSH, a partir da VPN da empresa e de um coworking.
- O Security Group libera a porta 22 para qualquer origem. A instância usa par de chaves, sem login por senha.
- O CloudTrail está habilitado na região e os VPC Flow Logs estão ativos nessa VPC.
- Ainda não verifiquei: se alguma tentativa de login teve sucesso, se o IP de origem aparece em outros achados e se havia algum teste de segurança autorizado nesse período.

4. Estrutura obrigatória da resposta
Responda sempre nesta ordem:
1. Explique o significado do alerta em linguagem simples.
2. Apresente as possíveis causas (hipóteses), da mais provável para a menos provável.
3. Para cada hipótese, diga qual evidência a confirma e qual a descarta.
4. Informe em quais serviços e registros da AWS essas evidências podem ser encontradas (nome do serviço e do log).
5. Apresente medidas de contenção, separando ações reversíveis das irreversíveis.
6. Liste as informações que ainda faltam para concluir a investigação.

5. Regras obrigatórias
- Use somente as informações que eu forneci.
- Nunca invente ID de instância, endereço IP, país de origem, número de conta, horário ou configuração.
- Marque como hipótese tudo que não vier dos dados que eu dei, e diferencie claramente fatos confirmados de hipóteses.
- Nunca classifique um alerta como falso positivo sem dizer qual evidência sustentaria essa conclusão.
- Antes de recomendar uma ação que possa interromper serviços, derrubar acesso ou revogar credencial, explique o impacto dela em uma linha.
- Não recomende exclusão de recursos sem avaliar os riscos.
- Priorize medidas que preservem a disponibilidade do ambiente.
- Se faltar informação para alguma etapa, diga exatamente quais dados são necessários em vez de preencher.
```

---

## Passo 3: Prompt final (Passo 1 + Passo 2 unidos)

Este é o bloco que você cola na IA e que deve ser entregue na DIO.

```text
Você é um analista de segurança em nuvem especializado em AWS e vai me ajudar a investigar um achado do Amazon GuardDuty.

1. Descrição do achado
- Tipo: UnauthorizedAccess:EC2/SSHBruteForce
- Recurso afetado: instância EC2 em sub-rede pública, que hospeda o painel administrativo de testes de uma loja virtual
- Severidade: 2.0, baixa
- Quando: entre 01h30 e 02h50 de uma quarta-feira, horário de Brasília
- O que o GuardDuty descreve: tentativas repetidas de autenticação SSH na porta 22, partindo de um único endereço IP externo, durante cerca de oitenta minutos

2. Público-alvo
- Quem vai ler a análise: profissional de infraestrutura responsável pelo monitoramento da AWS, com bom conhecimento de Linux e conhecimento básico de segurança em nuvem.
- O que eu preciso ao final: decidir se bloqueio o acesso SSH à instância agora ou se continuo investigando antes de agir.

3. Contexto do ambiente, até onde consigo confirmar hoje
- A instância hospeda o painel de testes. Se sair do ar, o time de desenvolvimento perde o ambiente por algumas horas, mas nenhum cliente é afetado.
- Quem acessa: apenas o time de desenvolvimento (5 pessoas), por SSH, a partir da VPN da empresa e de um coworking.
- O Security Group libera a porta 22 para qualquer origem. A instância usa par de chaves, sem login por senha.
- O CloudTrail está habilitado na região e os VPC Flow Logs estão ativos nessa VPC.
- Ainda não verifiquei: se alguma tentativa de login teve sucesso, se o IP de origem aparece em outros achados e se havia algum teste de segurança autorizado nesse período.

4. Estrutura obrigatória da resposta
Responda sempre nesta ordem:
1. Explique o significado do alerta em linguagem simples.
2. Apresente as possíveis causas (hipóteses), da mais provável para a menos provável.
3. Para cada hipótese, diga qual evidência a confirma e qual a descarta.
4. Informe em quais serviços e registros da AWS essas evidências podem ser encontradas (nome do serviço e do log).
5. Apresente medidas de contenção, separando ações reversíveis das irreversíveis.
6. Liste as informações que ainda faltam para concluir a investigação.

5. Regras obrigatórias
- Use somente as informações que eu forneci.
- Nunca invente ID de instância, endereço IP, país de origem, número de conta, horário ou configuração.
- Marque como hipótese tudo que não vier dos dados que eu dei, e diferencie claramente fatos confirmados de hipóteses.
- Nunca classifique um alerta como falso positivo sem dizer qual evidência sustentaria essa conclusão.
- Antes de recomendar uma ação que possa interromper serviços, derrubar acesso ou revogar credencial, explique o impacto dela em uma linha.
- Não recomende exclusão de recursos sem avaliar os riscos.
- Priorize medidas que preservem a disponibilidade do ambiente.
- Se faltar informação para alguma etapa, diga exatamente quais dados são necessários em vez de preencher.

6. Resultado esperado
Uma análise clara, organizada e tecnicamente fundamentada, que ajude a equipe a avaliar o risco e tomar uma decisão segura, sem conclusões precipitadas e sem dados inventados.

Se algum dado necessário para concluir não estiver acima, pergunte antes de responder.
```

---

## Testes de validação (feitos depois de rodar o prompt)

**Teste 1: o achado como descrito.**
Esperado: a resposta segue as 6 etapas, separa fato de hipótese e cita serviços e logs (CloudTrail, VPC Flow Logs, página do achado no GuardDuty, `/var/log/auth.log` ou `/var/log/secure` na instância).

**Teste 2: pergunta sem dado disponível.** Na mesma conversa, envie:

```text
Qual é o endereço IP de origem e o ID da instância?
```

Esperado: a IA diz que não tem esses dados e indica onde encontrá-los (detalhes do achado no console do GuardDuty).

**Teste 3: caso ambíguo.** Em uma conversa nova, troque a seção 1 por:

```text
- Tipo: Policy:IAMUser/RootCredentialUsage
- Recurso afetado: usuário root da conta AWS
- Severidade: 5.0, média
- Quando: sábado, das 09h às 11h
- O que o GuardDuty descreve: uso das credenciais do usuário root para acessar o console
- O que eu ainda não verifiquei: se havia uma migração planejada nesse horário e quem na equipe tem acesso ao root
```

Esperado: a IA considera atividade autorizada como hipótese, pede evidências (CloudTrail, ticket da migração, IP de origem) e não crava que existe um incidente.

**Checklist final**
- [ ] A ordem das 6 etapas se manteve nos três testes
- [ ] As evidências citam serviço e log, não apenas "verifique os registros"
- [ ] A contenção separa o reversível (restringir a porta 22 aos IPs conhecidos) do irreversível (encerrar a instância)

---

## Como entregar

1. Salve este arquivo como `.md` (ou só o prompt final como `.txt`).
2. Publique no Google Drive (Acesso geral: "Qualquer pessoa com o link"), no GitHub (repositório público) ou no Notion (publicar na web).
3. Copie a URL do arquivo já aberto e confira numa aba anônima.
4. Cole o link em **Enviar link** na DIO.
