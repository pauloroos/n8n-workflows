# Resumo Tecnico Diario

Workflow n8n que envia automaticamente um e-mail diario com as principais noticias de tecnologia e lancamentos de ferramentas, filtrados por IA com base nos seus interesses.

## O que ele faz

Todo dia as 8h da manha o workflow:

1. Busca os ultimos itens de 16 feeds RSS (9 de noticias + 7 de ferramentas/produtos)
2. Converte tudo em CSV e envia para o Google Gemini
3. O Gemini seleciona os 10-15 itens mais relevantes de cada categoria com base em palavras-chave de interesse
4. Formata tudo em um e-mail HTML bonito e envia para sua caixa de entrada

## Fluxo

```
Agendamento (08h)
    ├── Tech News Sites (9 feeds) → Loop → RSS Read → Sort → Limit
    └── Tools & Products (7 feeds) → Loop → RSS Read → Sort → Limit
                                          ↓
                                   Unir as Listas
                                          ↓
                                   Converter para CSV
                                          ↓
                                   Subir Arquivo no Gemini
                                          ↓
                                   Analisar o Documento (Gemini 2.5 Flash)
                                          ↓
                                   Formatar HTML (JavaScript)
                                          ↓
                                   Enviar E-mail (Gmail SMTP)
```

## Fontes monitoradas

### Noticias de Tecnologia (9 fontes)
- Ars Technica
- The Verge
- Wired
- MIT Technology Review
- TechCrunch
- CanalTech (BR)
- Tecnoblog (BR)
- Inovacao Tecnologica (BR)
- Science Daily — Technology

### Ferramentas & Produtos (7 fontes)
- Reddit r/SideProject
- Reddit r/InternetIsBeautiful
- dev.to — tag tools
- Product Hunt
- Hacker News Launches
- Hacker News Show HN
- TechCrunch — SaaS

## Credenciais necessarias

| Credencial | Como obter |
|---|---|
| Google Gemini API | console.cloud.google.com — o plano gratuito e suficiente |
| Gmail SMTP | Conta Gmail com senha de app habilitada (Google Account → Security → App passwords) |

## Como importar

1. No n8n, va em **Settings → Import Workflow** (ou use o atalho)
2. Selecione o arquivo `01. Resumo Tecnico Diario.json`
3. Configure as credenciais nos nos **Subir Arquivo no Gemini**, **Analisar o Documento** e **Enviar E-mail**
4. No no **Enviar E-mail**, atualize os campos `fromEmail` e `toEmail` com seus enderecos
5. Ative o workflow

## Como personalizar

- **Fontes RSS**: edite os nos `Tech News Sites` e `Tools Subredit and Sites` com os feeds que voce quiser
- **Palavras-chave de interesse**: edite o prompt no no `Analisar o Documento` — procure o campo `text` e altere as listas de keywords
- **Horario de envio**: edite o no `Envio Diario as 08h` e mude o `triggerAtHour`
- **Quantidade de itens**: os nos `Limit` e `Limit 10` controlam quantos itens de cada feed sao processados (padrao: 5 por feed)

## Modelo de IA

Usa **Gemini 2.5 Flash** por padrao. Pode ser trocado para qualquer modelo disponivel na API do Google Gemini editando o campo `modelId` no no `Analisar o Documento`.
