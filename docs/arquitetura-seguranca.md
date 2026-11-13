# Arquitetura e diretrizes técnicas

## Arquitetura escolhida
A proposta é um monólito organizado em camadas, utilizando o padrão MVT (Model-View-Template) do Django. As regras de negócio devem ficar em módulos de serviços, evitando concentrar lógica complexa nas views.

### Camadas previstas
- **Apresentação:** templates HTML, CSS e Bootstrap 5.3; interface responsiva.
- **Aplicação:** views, formulários, autenticação e autorização.
- **Serviços de domínio:** regras de reincidência em sete dias, atualização de status, validações e preparação de alertas.
- **Persistência:** ORM do Django, SQLite no desenvolvimento local e PostgreSQL 16 no ambiente hospedado.
- **PWA:** Web App Manifest, Service Worker e fila local de sincronização.

## Tecnologias planejadas
| Tecnologia | Uso |
|---|---|
| Python 3.12 | Linguagem principal |
| Django 5.2 LTS | Backend |
| PostgreSQL 16 | Banco hospedado |
| SQLite | Desenvolvimento local |
| Bootstrap 5.3 | Interface responsiva |
| Service Worker | Cache e suporte offline |
| Web App Manifest | Instalação como PWA |
| pytest-django 4.x | Testes automatizados |
| Gunicorn 23.x | Servidor WSGI |

As versões são decisões registradas no planejamento e devem ser verificadas no momento da instalação e publicação.

## Fluxo offline previsto
1. O técnico preenche o formulário no dispositivo.
2. A aplicação gera um codigo_envio único.
3. Sem conexão, o registro fica em fila local.
4. Quando a conexão retornar, a aplicação envia os registros pendentes.
5. O servidor verifica o identificador único antes de criar o chamado.
6. A interface informa o resultado da sincronização e mantém pendências visíveis em caso de falha.

O armazenamento local, a política de expiração e o tratamento de conflitos ainda deverão ser detalhados e testados. Não armazenar dados pessoais além do necessário.

## Segurança
- Autenticação obrigatória e perfis técnico, suporte e gestor.
- Autorização validada no servidor em cada operação.
- Senhas protegidas pelo mecanismo do Django (PBKDF2-SHA256).
- HTTPS em produção; cookies de sessão com configurações seguras.
- DEBUG=False em produção.
- Segredos e credenciais fornecidos por variáveis de ambiente.
- ORM para consultas parametrizadas.
- Escape automático dos templates; não marcar entrada do usuário como segura sem sanitização.
- Mensagens de erro genéricas e logs sem credenciais ou dados pessoais desnecessários.
- Dependências verificadas antes do deploy, incluindo auditoria de vulnerabilidades.

## Desempenho
Metas iniciais:
- Formulário com resposta inferior a três segundos, medida pela mediana de cinco execuções após aquecimento.
- Painel carregado em até cinco segundos no cenário definido.
- Paginação de 20 registros.
- Índices para campos usados em filtros e relacionamentos.
- Recursos estáticos minificados e cache controlado pelo Service Worker.

As medições devem registrar dispositivo, rede, quantidade de dados de teste, data e commit avaliado. Não declarar metas atingidas antes de executar os testes.

## Decisões pendentes
- Provedor e plano de hospedagem.
- Configuração final de produção e pipeline de deploy.
- Estratégia de bloqueio de tentativas de login e backend de cache.
- Política de retenção dos dados.
- Estratégia completa de sincronização e resolução de conflitos.
