# n8n Workflows — Automacoes que uso no dia a dia

Repositorio publico com workflows n8n prontos para usar. Cada workflow tem documentacao propria, arquivo JSON para importar direto no n8n e instrucoes de configuracao.

## Workflows disponiveis

| Workflow | Descricao | Integrações |
|---|---|---|
| [Resumo Tecnico Diario](./workflows/resumo-tecnico-diario/) | Newsletter diaria automatizada com curadoria de IA | RSS + Gemini AI + Gmail |

## Em breve

- Resumo de PRs e issues do GitHub com IA
- Notificacoes de deploy com resumo de mudancas
- Digest semanal de artigos salvos no Pocket/Instapaper

## Como usar

1. Acesse a pasta do workflow que te interessa
2. Leia o `README.md` do workflow para entender o que ele faz e o que precisa configurar
3. Importe o arquivo `.json` no seu n8n (Settings → Import Workflow)
4. Configure as credenciais conforme descrito
5. Ative o workflow

## Estrutura do repositorio

```
workflows/
└── resumo-tecnico-diario/
    ├── README.md        ← Documentacao e instrucoes
    └── *.json           ← Arquivo do workflow para importar
```

## Licenca

MIT — use, modifique e distribua livremente.

---

Se algum workflow te ajudou, deixa uma ⭐ no repositorio.
