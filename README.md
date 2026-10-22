# INKIS IA V8.1 — Inteligência Estendida Local

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
