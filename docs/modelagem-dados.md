# Modelo conceitual de dados

Esta modelagem é inicial e deverá ser refinada durante a implementação e validada com o parceiro. Não representa migrações ou tabelas já implementadas.

## Entidades

### Região
- id: identificador.
- nome: obrigatório e único.
- tipo: condomínio, rua ou vila.

### Cliente
- id: identificador.
- nome: obrigatório.
- endereço: necessário ao atendimento.
- telefone: opcional.
- regiao_id: referência à região.
- ativo: indica se o cadastro está ativo.

### Técnico/usuário
- id: identificador.
- nome: obrigatório.
- usuario: identificador de login único.
- senha_hash: hash gerado pelo mecanismo de autenticação do Django; nunca armazenar senha em texto puro.
- perfil: técnico, suporte ou gestor.
- ativo: indica se o acesso está ativo.

### Chamado
- id: identificador interno.
- codigo_envio: identificador único criado no dispositivo para evitar duplicidade na sincronização offline.
- cliente_id: referência ao cliente.
- tecnico_id: referência ao usuário responsável pelo registro.
- abertura_em: data/hora de abertura.
- tipo_falha: sem sinal, lentidão, queda intermitente ou outro.
- descricao: texto de até 500 caracteres.
- status: aberto, em atendimento ou resolvido.
- solucao_aplicada: obrigatória ao resolver.
- resolvido_em: data/hora da resolução.
- reincidente: informação calculada a partir da existência de chamado anterior do mesmo cliente nos sete dias anteriores.

## Relacionamentos
- Região 1:N Cliente — uma região pode possuir vários clientes; cada cliente pertence a uma região.
- Cliente 1:N Chamado — um cliente pode possuir vários chamados; cada chamado pertence a um cliente.
- Técnico 1:N Chamado — um técnico/usuário pode registrar vários chamados; cada chamado referencia o responsável pelo registro.

## Restrições e decisões
- Não excluir fisicamente chamados ou clientes no fluxo operacional; utilizar inativação quando necessário.
- Não coletar CPF, dados bancários ou GPS.
- O código de envio deve possuir restrição de unicidade no banco.
- A reincidência deve considerar a janela de sete dias anterior à abertura do chamado.
- Garantir integridade das referências no banco e na camada de aplicação.

## Evoluções possíveis
Entidades de medição de conexão e alerta podem ser avaliadas após validação do MVP. Não fazem parte do modelo mínimo atual.

## Próximas decisões
- Confirmar campos obrigatórios de endereço com o parceiro.
- Definir política de retenção e acesso ao histórico.
- Especificar fuso horário e tratamento de datas na sincronização offline.
- Detalhar como conflitos de sincronização serão apresentados.
- Elaborar MER/DER e normalização conforme o conteúdo efetivamente exigido na Unidade 2.
