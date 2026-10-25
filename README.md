# INKIS IA V10.1 — Ollama Mobile Ready

Preserva a V10 e corrige a configuração do Ollama no Android.

## O que mudou
- detecta Android usando 127.0.0.1/localhost;
- explica que localhost aponta para o próprio telefone;
- campos separados para IP do computador e porta;
- monta automaticamente `http://IP:11434`;
- botão para abrir `/api/tags`;
- teste real da API local com timeout;
- lista modelos encontrados;
- avisa sobre HTTPS→HTTP (mixed content);
- evita tentativa automática repetida de localhost no Android;
- mantém Gemini como alternativa remota gratuita quando disponível.

## O que ainda precisa ser feito no computador
O INKIS IA não pode alterar remotamente o firewall ou a configuração do processo Ollama. O computador deve aceitar conexões da rede local e permitir a porta 11434 na rede privada.
