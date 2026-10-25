# INKIS IA V10.3 — Compatibilidade offline e QA

Base: V10.2 Auth Recovery, preservando recuperação Supabase, Ollama, central de ferramentas, exportação de projetos e interface.

## Novidades V10.3
- Cópia resiliente nas mensagens, Prompt Lab e Text Lab: Clipboard API em contexto seguro, tentativa alternativa via seleção/execCommand e, se bloqueada, campo para seleção manual com opção de baixar TXT.
- Instruções reforçadas do gerador: aplicativos standalone não podem depender somente de `navigator.clipboard.writeText`; devem oferecer alternativas claras em `content://`/`file://`.
- QA estrutural passa a identificar o risco conhecido de clipboard sem fallback e apresenta escopo **estático**, não confundido com testes funcionais no Android.
- Reparo automático de aplicativo recebe as regras de compatibilidade; um reparo que continue falhando não substitui o original.
- Service Worker com novo identificador de cache para atualização do PWA hospedado.

## Implantação
Extraia o ZIP, preserve a estrutura das pastas e publique todos os arquivos (incluindo `index.html`, `manifest.webmanifest`, `service-worker.js`, `assets/`, `icons/`). Para uso com Gemini, a autenticação e a Edge Function existentes continuam necessárias.

A V10.3 não altera nem publica automaticamente o aplicativo que está no GitHub Pages. Substitua os arquivos de implantação e atualize a página. As informações existentes no `localStorage` do navegador não são apagadas pela instalação normal, mas convém exportar os projetos antes da atualização.

## Limitações
Um teste estático não confirma botões em execução. O comportamento real de `navigator.clipboard` varia por navegador, permissões e contexto (especialmente Android `content://`). Quando o próprio navegador bloqueia todas as tentativas de cópia, apenas selecionar manualmente ou baixar TXT é confiável.

© 2026 Nailson Lima. Termos de uso e política de privacidade preservados.
