# Contexto, problema e escopo do MVP

## Origem da demanda
A demanda foi levantada em conversa semiestruturada com Rodrigo, sócio principal da Megapcnet, complementada por observação contextual e pela experiência anterior do aluno em instalação de internet/telecomunicações na região de Perus (São Paulo).

A data exata da entrevista e o sobrenome do contato permanecem pendentes de confirmação. Não preencher esses dados por suposição.

## Problema observado
- Reclamações de perda de sinal e instabilidade.
- Chamados recebidos principalmente pelo WhatsApp.
- Encaminhamento de técnicos após a reclamação, caracterizando atendimento reativo.
- Alguns clientes voltam a relatar problemas depois de uma visita.
- Ausência de histórico organizado por cliente e região.
- Interesse do parceiro em identificar instabilidades antes das reclamações, com possível uso futuro de IA.

Foi mencionada uma estimativa inicial de aproximadamente 8% de clientes com reclamações, com destaque para um condomínio próximo a uma comunidade. A estimativa não é indicador auditado e precisa ser validada com dados consistentes.

## Objetivo do produto
Disponibilizar uma aplicação web instalável (PWA), simples e adequada ao celular, que organize registros de atendimento e ofereça à gestão uma visão histórica por cliente, região e período.

## Escopo funcional
1. Cadastro/consulta de clientes e regiões necessários ao registro.
2. Registro de chamado com tipo de falha, descrição, cliente, técnico e data/hora.
3. Atualização de status e inclusão da solução aplicada ao concluir o atendimento.
4. Consulta do histórico por cliente.
5. Identificação de reincidência quando existir chamado anterior do mesmo cliente nos sete dias anteriores.
6. Painel gerencial por região e período.
7. Armazenamento offline e sincronização posterior, com identificador único de envio.

## Priorização
**Obrigatório:** registro, atualização de status/solução, histórico/reincidência e painel por região.

**Requisito técnico do fluxo móvel:** registro offline e sincronização sem duplicidade.

**Desejável/evolutivo:** alerta preventivo simples, por exemplo, sinalizar três chamados na mesma região em 24 horas. A regra precisa ser validada com o parceiro e não equivale a previsão por IA.

## Fora do escopo
- Aplicativo nativo para lojas; a proposta é PWA.
- Integração com API do WhatsApp.
- Integração com cobrança ou financeiro.
- Monitoramento em tempo real de toda a rede.
- IA avançada ou modelo preditivo treinado.
- Diagnóstico automático da causa física da falha.
- GPS ou rastreamento de clientes e técnicos.

## Usuários e contexto
**Diretos:** técnicos de campo e atendentes de suporte, com uso predominante em celular, possivelmente com uma mão, iluminação variável, conexão instável e pouco tempo. Meta de registro inferior a um minuto. O gestor consulta o painel e acompanha reincidências.

As faixas etárias de 20 a 40 anos são estimativas do levantamento inicial, não dados demográficos validados.

**Indiretos:** moradores e clientes atendidos em Perus, incluindo moradores de condomínios, estudantes, trabalhadores remotos e pequenos comerciantes.

## Princípios
- Priorizar tarefas rápidas e linguagem clara.
- Funcionar em telas pequenas e suportar conectividade instável.
- Não depender de cor isolada para comunicar status ou atenção.
- Manter histórico de chamados e evitar exclusão física de registros.
- Coletar apenas dados necessários à finalidade do sistema.
- Separar indicadores observados de hipóteses e metas ainda não validadas.
