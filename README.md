# Painel de IA V7 — Multiengine

Esta versão oferece três motores:

1. **Ollama local** — sem cobrança por token.
2. **Google Gemini** — pelo backend Supabase; pode operar sem cobrança enquanto a conta estiver no Free Tier e dentro das cotas.
3. **OpenAI** — opcional e somente manual; nunca é usada como fallback automático.

## Backend já atualizado

A Edge Function `painel-ia` do projeto Supabase `Painel-Lima-Virtual` foi atualizada para a arquitetura V7.

- `provider: auto` → Gemini somente quando configurado; não usa OpenAI.
- `provider: gemini` → força Gemini.
- `provider: openai` → força OpenAI.
- Ollama é chamado diretamente pelo navegador, porque roda no equipamento/rede do usuário.

## Ativar Gemini Free Tier

No Supabase, abra **Edge Functions → Secrets** e adicione:

- `GEMINI_API_KEY` = sua chave do Google AI Studio
- opcionalmente `GEMINI_MODEL` = `gemini-3.8-flash`

A elegibilidade e as cotas gratuitas são controladas pelo Google e podem mudar. O painel exibe `R$ 0,00*` como indicação condicional, não como garantia de gratuidade.

## Ollama

Endpoint padrão: `http://127.0.0.1:11434`.

A V7 consulta `/api/tags` para localizar modelos instalados e usa `/api/chat` para as respostas.

Exemplo:

```text
ollama pull gemma3:4b
```

Depois, abra o painel, selecione **Ollama**, clique em **Testar Ollama** e escolha o modelo encontrado.

### Android + computador

O Android pode usar o Ollama que está rodando em outro computador da rede. Informe no painel o endereço, por exemplo `http://192.168.1.20:11434`.

O Ollama precisa estar configurado para escutar na rede local e permitir a origem web necessária. Restrinja o acesso à rede privada; não exponha a porta 11434 diretamente à internet.

Uma página HTTPS pode bloquear chamadas diretas para um endpoint Ollama HTTP por mixed content. Nessa situação use Gemini ou coloque o Ollama atrás de HTTPS com autenticação e controles de rede adequados.

## Windows

A versão oficial atual do Ollama para Windows exige Windows 10 ou posterior. Para Windows 7, use o Gemini pelo painel ou execute Ollama em outro computador compatível.

## Segurança

- `GEMINI_API_KEY` e `OPENAI_API_KEY` nunca ficam no HTML.
- A Edge Function exige JWT válido do Supabase.
- A chave publicável do Supabase fica no frontend, como previsto para clientes.
- OpenAI nunca é fallback do modo Automático.
- Histórico, preferências e estatísticas de sessão são mantidos localmente no navegador.

## Teste de aceite

**Ollama:** iniciar Ollama → baixar modelo → Testar Ollama → enviar `Responda apenas: Ollama conectado`.

**Gemini:** cadastrar `GEMINI_API_KEY` no Supabase → entrar no painel → selecionar Gemini → enviar `Responda apenas: Gemini conectado`.

**Automático:** Ollama disponível deve ser priorizado; sem Ollama, deve usar Gemini; sem ambos, deve informar indisponibilidade. Nunca deve acionar OpenAI automaticamente.
