# INKIS IA V10.2 — Recuperação de Sessão

Correção específica para o problema observado no GitHub Pages.

## Diagnóstico confirmado
Os logs reais do Supabase registraram `refresh_token_not_found` ao tentar renovar a sessão no Android.
A Edge Function `painel-ia` continua ACTIVE, versão 6.

## Correções V10.2
- sessão inválida é removida automaticamente;
- refresh token ausente/inválido não fica preso no localStorage;
- status do sistema diferencia “sem login” de “GEMINI_API_KEY ausente”;
- Gemini não aparece mais como “PENDENTE” apenas porque o backend não pôde ser consultado;
- Backend mostra “Aguardando login válido” quando a sessão expirou;
- botão “Entrar novamente” no diagnóstico;
- login bem-sucedido limpa o aviso de sessão;
- dados locais, projetos, memória e biblioteca não são apagados ao limpar a sessão.
