# Auto-revisão técnica do MVP

## Escopo desta revisão

Esta revisão considera os artefatos de planejamento atualmente versionados no repositório: escopo do MVP, requisitos, modelagem de dados, arquitetura e segurança e plano de validação. O projeto ainda está na etapa de preparação técnica; a aplicação Django não foi implementada. Portanto, esta análise não afirma que testes de código, desempenho ou segurança já foram executados.

## Arquitetura e modularização

A decisão atual é manter um monólito organizado em camadas, com Django 5.2 LTS e padrão MVT. Para o porte e o escopo do MVP, essa estrutura evita a complexidade operacional de microsserviços e permite evoluir o sistema em uma única aplicação. As regras de negócio — como cálculo de reincidência em sete dias e geração de alertas — devem ficar em módulos de serviços, separadas das views e dos templates. Isso reduz duplicação e facilita testes unitários.

## Modelagem e integridade

A revisão confirmou as relações Região 1:N Cliente, Cliente 1:N Chamado e Técnico 1:N Chamado. O campo codigo_envio único foi previsto para que a sincronização de registros feitos offline não gere chamados duplicados. A reincidência deve ser calculada a partir dos chamados do mesmo cliente nos sete dias anteriores, em vez de ser tratada como um dado digitado manualmente. Chamados não devem ser apagados: o encerramento e a inativação preservam o histórico operacional.

## Segurança

O acesso deve exigir autenticação e respeitar perfis de técnico, suporte e gestor. As senhas serão armazenadas pelo mecanismo PBKDF2-SHA256 do Django, nunca em texto puro. A camada de dados usará o ORM para consultas parametrizadas; templates manterão o escape automático para reduzir risco de XSS. Em produção, DEBUG ficará desativado, segredos serão fornecidos por variáveis de ambiente e o acesso deverá ocorrer por HTTPS. A autorização precisa ser verificada no servidor em cada operação, não apenas pela ocultação de botões na interface.

## Desempenho e uso offline

O registro de chamado é a operação prioritária e deve funcionar em celular, inclusive com conexão instável. A PWA usará Service Worker e fila local de sincronização; o identificador codigo_envio permitirá reconhecer reenvios. Para o painel, foram previstos paginação de 20 registros e índices nos campos usados em filtros e relacionamentos. As metas de tempo descritas no plano de validação ainda precisam ser medidas em ambiente controlado, com dados fictícios.

## Pontos de atenção e próximos passos

- Implementar primeiro o fluxo de registro e atualização de chamados antes de avançar para o painel.
- Testar a sincronização offline com perda de conexão e reenvio da mesma operação.
- Validar permissões por perfil e tentativas de acesso direto a operações restritas.
- Medir os tempos com o cenário de teste documentado e registrar os resultados reais.
- Revisar os requisitos desejáveis de alerta preventivo sem apresentá-los como funcionalidade já implementada.

## Resultado da auto-revisão

A arquitetura proposta é compatível com o tamanho atual do MVP e mantém separadas apresentação, regras de negócio e persistência. Os principais riscos identificados são duplicidade na sincronização offline, falhas de autorização por perfil e concentração de regras nas views. As decisões acima reduzem esses riscos no desenho, mas sua eficácia só poderá ser confirmada após a implementação e os testes.