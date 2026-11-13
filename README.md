# MEGAPCNET — Sistema de apoio ao registro e acompanhamento de chamados técnicos

> **Nome de trabalho:** MEGAPCNET — Sistema de Apoio ao Registro e Acompanhamento de Chamados Técnicos. O nome definitivo do projeto acadêmico ainda precisa ser confirmado e deverá permanecer igual ao utilizado na Experiência Prática 1.

## Contexto
Projeto acadêmico de Análise e Desenvolvimento de Sistemas, baseado em uma demanda apresentada pela Megapcnet, pequeno provedor de internet que atende Perus, São Paulo.

O levantamento inicial apontou reclamações de perda de sinal e instabilidade. Os contatos chegam principalmente pelo WhatsApp e o atendimento é reativo, com encaminhamento de técnicos. Há relatos de reincidência após visitas. Foi mencionada uma estimativa de aproximadamente 8% de clientes com reclamações, especialmente em um condomínio da região. Esse percentual é uma referência relatada, ainda não validada por uma base organizada.

Também foi identificada a ausência de histórico centralizado por cliente e região. O parceiro manifestou interesse em utilizar IA para identificar instabilidades antes das reclamações.

## Objetivo
Planejar e desenvolver um Progressive Web App (PWA), com foco no celular, para registrar e acompanhar chamados técnicos, organizar o histórico por cliente e região e apoiar decisões gerenciais.

A prioridade do MVP é estruturar os dados e as regras simples de acompanhamento. IA avançada e monitoramento em tempo real de toda a rede não fazem parte do protótipo inicial.

## Escopo inicial
- Registrar chamados vinculados a clientes, técnicos e regiões.
- Atualizar status e registrar a solução aplicada.
- Consultar histórico por cliente.
- Identificar reincidência quando houver chamado anterior do mesmo cliente nos sete dias anteriores.
- Exibir painel gerencial por região e período.
- Permitir registro offline e sincronização posterior sem duplicidade.
- Considerar alertas preventivos simples como evolução desejável, não como funcionalidade já implementada.

## Fora do escopo
- Aplicativo nativo publicado nas lojas; a proposta é PWA.
- Integração com API do WhatsApp ou cobrança.
- Monitoramento em tempo real de toda a rede.
- IA avançada para previsão de falhas.
- Coleta de GPS de clientes ou técnicos.

## Tecnologias planejadas
| Camada | Tecnologia |
|---|---|
| Linguagem | Python 3.12 |
| Backend | Django 5.2 LTS |
| Banco de produção | PostgreSQL 16 |
| Banco local | SQLite |
| Interface | HTML, CSS e Bootstrap 5.3 |
| PWA | Web App Manifest e Service Worker |
| Testes | pytest e pytest-django 4.x |
| Servidor WSGI | Gunicorn 23.x |

As tecnologias representam decisões do planejamento; configuração e implementação ainda precisam ser realizadas e testadas.

## Documentação
- [Escopo e contexto do MVP](docs/escopo-mvp.md)
- [Requisitos funcionais e não funcionais](docs/requisitos.md)
- [Modelo conceitual de dados](docs/modelagem-dados.md)
- [Arquitetura e segurança](docs/arquitetura-seguranca.md)
- [Plano de validação e indicadores](docs/plano-validacao.md)

## Situação atual
**Etapa:** organização e documentação inicial. Este repositório ainda não representa uma aplicação funcional. As telas são protótipos planejados e as validações com o parceiro estão previstas; não devem ser interpretadas como testes já realizados.

## Dados e privacidade
A documentação utiliza informações do levantamento inicial e dados demonstrativos. Não adicionar nomes, telefones, endereços detalhados, conversas ou outros dados pessoais reais de clientes. Utilizar somente dados fictícios para desenvolvimento e demonstração.
