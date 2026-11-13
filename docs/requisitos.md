# Requisitos do sistema

## Requisitos funcionais

| ID | Requisito | Prioridade | Dependências / observações |
|---|---|---|---|
| RF01 | Registrar chamado vinculado a cliente, técnico e região, com tipo de falha e descrição. | Obrigatório | Base do atendimento. |
| RF02 | Guardar registro offline e sincronizar sem duplicidade. | Obrigatório | Depende do RF01; usar código único gerado no dispositivo. |
| RF03 | Identificar reincidência quando o mesmo cliente possuir chamado nos sete dias anteriores. | Obrigatório | Regra calculada a partir do histórico. |
| RF04 | Atualizar status e registrar solução aplicada ao resolver. | Obrigatório | Solução obrigatória ao concluir. |
| RF05 | Exibir painel por região e período, restrito ao gestor. | Obrigatório | Depende dos dados do RF01 e da regra RF03. |
| RF06 | Sinalizar concentração de chamados, por exemplo, três chamados na mesma região em 24 horas. | Desejável | Evolução; não equivale a IA preditiva e não integra o protótipo inicial. |

### Ordem prevista
RF01 → RF04 → RF03 → RF02 → RF05 → RF06.

## Regras de negócio
- Um chamado pertence a um cliente e é registrado por usuário autorizado.
- Cada cliente pertence a uma região.
- Status previstos: aberto, em atendimento e resolvido.
- Ao resolver, a solução aplicada deve ser informada.
- Há reincidência quando existe chamado anterior do mesmo cliente nos sete dias que antecedem a abertura do novo chamado.
- O código de envio criado no dispositivo deve ser único para permitir sincronização idempotente.
- Clientes e chamados não devem ser apagados fisicamente no fluxo operacional; quando aplicável, clientes podem ser inativados.

## Requisitos não funcionais

### RNF01 — Segurança e acesso
- Exigir autenticação.
- Aplicar perfis: técnico, suporte e gestor.
- Armazenar senhas com o mecanismo padrão seguro do Django (PBKDF2-SHA256), nunca em texto puro, MD5 ou SHA-1.
- Planejar sessão com duração máxima de oito horas e cookies HttpOnly, Secure em HTTPS e SameSite.
- Apresentar mensagens genéricas de erro de autenticação.
- Planejar bloqueio temporário de 15 minutos após cinco tentativas malsucedidas, com mecanismo de cache apropriado.
- Exigir troca de senha temporária no primeiro acesso; comprimento mínimo previsto de oito caracteres. Reavaliar a política conforme orientação de segurança vigente.

### RNF02 — Integridade, privacidade e validação
- Validar dados no cliente e obrigatoriamente no servidor.
- Utilizar ORM e consultas parametrizadas.
- Manter escape automático e evitar uso inseguro de filtros que desativem escape.
- Verificar autorização em cada operação, não apenas ocultar botões.
- Exibir erros sem expor detalhes internos.
- Minimizar dados: não coletar CPF, dados bancários ou GPS.
- Manter segredos em variáveis de ambiente, fora do código e do histórico Git.
- Verificar dependências e vulnerabilidades antes de publicar.

### RNF03 — Desempenho e ambiente
- Hospedagem planejada em ambiente compatível com Python e PostgreSQL gerenciado; provedor ainda a definir.
- Configuração por variáveis de ambiente.
- Documentar instalação e execução.
- Meta do formulário: menos de três segundos, mediana de cinco medições após aquecimento.
- Meta do painel: até cinco segundos no cenário de teste definido.
- Cenário-alvo: Android com 2 GB de RAM, Chrome, rede Slow 4G e base fictícia com 200 clientes e 1.000 chamados.
- Otimizações previstas: paginação de 20 itens, índices, recursos estáticos minificados e cache via Service Worker.

### RNF04 — Acessibilidade e usabilidade
- Alvos de toque de pelo menos 44 × 44 px.
- Contraste mínimo de 4,5:1 para texto comum e 3:1 para componentes e elementos gráficos aplicáveis.
- Suporte a zoom de 200% e viewport de 320 px.
- Campos com rótulos programáticos e visíveis.
- Foco visível e navegação por teclado.
- Mensagens de erro que expliquem como corrigir.
- Estados comunicados por texto e/ou ícone, nunca somente por cor.

## Segurança — ameaças a considerar
A análise inicial considera categorias do OWASP Top 10:2021:
- A01 — Broken Access Control: verificar permissão em cada operação.
- A03 — Injection: ORM e consultas parametrizadas.
- A03 — Cross-Site Scripting (XSS): escape automático, evitar conteúdo marcado como seguro sem sanitização e avaliar Content Security Policy.
- A07 — Identification and Authentication Failures: proteger autenticação, sessões e tentativas.
- A05/A02 — Security Misconfiguration e Cryptographic Failures: DEBUG desativado em produção, segredos protegidos e HTTPS.

A referência OWASP 2021 foi a edição adotada no planejamento inicial. Conferir a edição solicitada pela disciplina antes da entrega final.
