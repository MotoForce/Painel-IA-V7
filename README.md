# INKIS IA V9 — Completo

A V8 amplia a qualidade das respostas sem depender de uma API paga por padrão.

## O que é “Inteligência Estendida”

Não é um novo modelo treinado. É uma camada de orquestração que melhora o uso dos modelos disponíveis através de:

- memória local controlada pelo usuário;
- recuperação de conhecimento da biblioteca e anexos;
- classificação local do tipo de tarefa;
- múltiplas etapas de geração/revisão;
- QA local heurístico;
- roteamento multiengine;
- bloqueio de multipass quando OpenAI paga estiver selecionada, por padrão.

## Modos

### Rápido
1 chamada ao modelo.

### Profissional
2 chamadas:
1. geração;
2. revisão silenciosa e resposta final.

### Profundo
3 chamadas:
1. plano conciso/checklist;
2. resposta;
3. refinamento final.

### Auditoria
3 chamadas:
1. resposta;
2. auditoria concisa de falhas/omissões;
3. correção final.

As etapas internas não são mostradas como cadeia de pensamento. O usuário recebe somente a resposta final.

## Base de conhecimento local

A biblioteca e os anexos são divididos em trechos localmente. A V8 faz uma busca lexical local e envia somente os trechos mais relacionados ao pedido. Não exige embeddings pagos.

A busca lexical é útil, mas não é equivalente a um banco vetorial semântico. Para uma evolução futura, pode-se adicionar embeddings locais via Ollama.

## Memória local

As memórias são adicionadas e removidas manualmente pelo usuário e ficam no `localStorage` do navegador. A V8 não cria memórias ocultas automaticamente.

## Política de custo

- Ollama local: sem cobrança por token.
- Gemini: pode ser usado quando a conta estiver dentro da camada/cota gratuita aplicável.
- OpenAI: opcional e potencialmente paga.
- `Bloquear multipass pago` vem ativado. Se OpenAI estiver selecionada, modos Profissional/Profundo/Auditoria são reduzidos a uma única chamada para evitar multiplicar custos.

## QA local

O QA local faz verificações heurísticas sobre:
- resposta não vazia;
- ausência de placeholders;
- ausência de algumas respostas genéricas;
- ausência de promessas absolutas detectáveis;
- tamanho controlado.

O indicador `QA x/5` não é uma certificação de veracidade. É apenas um conjunto de verificações locais.

## Compatibilidade

O funcionamento multiengine existente da V7.1 foi preservado:
- Ollama;
- Gemini via Supabase;
- OpenAI manual via Supabase;
- modo Automático sem fallback pago.

## Privacidade

Biblioteca, memórias, conversas e fluxos locais ficam no navegador. Ao usar um provedor em nuvem, o contexto selecionado para a resposta é enviado ao provedor correspondente.


## Identificação autoral e documentos legais

Copyright aplicado no rodapé:

**© 2026 Nailson Lima. Todos os direitos reservados.**

Foram incorporados ao próprio aplicativo:
- Termos de Uso;
- Política de Privacidade.

Os dois documentos são acessíveis por links no rodapé e abrem em modais internos compatíveis com os modos claro e escuro.

Observação: os textos são uma base operacional coerente com as funções atuais da aplicação. Caso o INKIS IA seja comercializado em escala, trate dados pessoais de terceiros, processe pagamentos, realize analytics ou passe a operar sob obrigações contratuais/regulatórias específicas, é recomendável revisão jurídica dos documentos.


## Correção crítica V8.2

Os logs reais do Supabase mostraram falhas `503 UNAVAILABLE` do Gemini 3.8 Flash em períodos de alta demanda.

O backend `painel-ia` foi publicado como **versão 5-resilient**:
- retry automático para erros transitórios;
- Gemini 3.8 Flash permanece como principal;
- fallback gratuito para `gemini-3.5-flash`;
- nenhuma troca automática para OpenAI;
- mensagens distintas para sobrecarga temporária e cota esgotada.

A interface também foi tornada resiliente:
- se a primeira resposta foi obtida e apenas a revisão/refinamento falhar, a resposta válida é preservada;
- modos Profissional, Profundo e Auditoria não descartam mais conteúdo útil por falha de uma etapa posterior;
- o painel identifica quando respondeu em “modo resiliente”.


## Correção de cortes V8.3

A V8.3 aplica uma revisão responsiva global para celulares Android, inclusive telas de 320–400 px:

- `overflow-x` bloqueado no documento;
- todos os grids usam `minmax(0, 1fr)`;
- cards e textos recebem `min-width: 0`;
- engines e modos de inteligência mudam para 1 coluna em celulares estreitos;
- botões de Anexar/Buscar/Modelos reorganizam-se verticalmente quando necessário;
- navegação inferior usa 5 colunas flexíveis sem largura fixa nos rótulos;
- barra inferior respeita `safe-area-inset-bottom`;
- conteúdo ganha espaço inferior suficiente para não ficar atrás da navegação;
- modais ficam limitados à altura real da tela (`100dvh`);
- rodapé legal respeita safe areas;
- textos longos podem quebrar linha sem sair dos cards;
- conflito antigo que forçava 2 colunas abaixo de 390 px no modo escuro foi removido.


## Evolução V9

- Backend Supabase `painel-ia` versão 6: saída longa, retry e fallback gratuito `gemini-3.8-flash → gemini-3.6-flash → gemini-3.5-flash-lite`.
- Respostas comuns: até 8.192 tokens por padrão. Projetos: até 24.576 tokens, com continuação quando necessário.
- Modo Projeto/App: instrui geração de HTML standalone completo, faz QA local e tenta reparo automático quando o projeto vem incompleto.
- Projetos ficam salvos localmente e podem ser exportados em HTML, JSON ou ZIP. O ZIP é criado no navegador sem biblioteca paga ou serviço externo.
- Pré-visualização em iframe sandbox.
- Memória contextual agora seleciona memórias relacionadas ao pedido em vez de enviar tudo indiscriminadamente.
- QA geral verifica placeholders, cercas de código, finalização, repetição anormal e tamanho.
- QA de projetos verifica estrutura HTML, fechamento das tags, TODO/FIXME, CSS, cerca Markdown e sintaxe dos scripts inline não-module.
- OpenAI continua manual e o bloqueio de multipass pago permanece ativo por padrão.

Observação: o QA local detecta integridade estrutural, mas não substitui testes funcionais específicos de integrações externas.
