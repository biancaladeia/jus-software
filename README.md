# jus-software

Sistema web de gestão para escritório de advocacia: intimações do DJEN capturadas automaticamente, cálculo de prazos com calendário forense, geração de documentos e financeiro com divisão de honorários entre parceiros.

**Em produção desde outubro de 2026**, usado no dia a dia por uma advogada autônoma e seus parceiros. Construído por uma pessoa, do zero ao ar em cerca de 20 dias, com desenvolvimento orientado por IA (Claude Code).

---

## O problema

A advogada controlava tudo em planilhas e numa pasta do Google Drive por cliente: processos, prazos, honorários divididos com parceiros (nem sempre 50/50) e documentos. As intimações eram lidas uma a uma no diário oficial, e cada prazo era contado à mão, considerando feriados e suspensões de cada tribunal.

## A solução

Um sistema único, no computador e no celular, que:

- **Captura as intimações do DJEN** duas vezes por dia pela OAB da advogada e faz a triagem: se o processo já está cadastrado, a intimação vai para ele; se não está, fica "A classificar".
- **Sugere o prazo** com base no calendário forense (feriados, suspensões e recessos do TJBA e do TJSP, cada data com a fonte do ato oficial) e na regra do CPC. **O sistema nunca cria um prazo sozinho**: ele sugere, e a advogada confirma a data fatal.
- **Gera procurações, contratos e declarações** a partir de modelos do próprio escritório, preenchidos com os dados do cliente e do processo. Se falta algum dado, o documento é bloqueado e o sistema avisa o que falta.
- **Controla o financeiro**: honorários iniciais (em R$ ou em salários mínimos), êxito, sucumbência e avulsos, com divisão automática entre a titular e até dois parceiros.
- **Controla o acesso por perfil**: a titular vê tudo; cada parceiro vê só os processos em que participa, e nunca vê o financeiro.

## Telas

<div align="center">

### Painel (computador)
<img width="776" height="502" alt="Painel do sistema no computador" src="https://github.com/user-attachments/assets/2c7b32cb-baf3-4d22-b97c-4f70062a2a9e" />

### Intimações e sugestão de prazo
<img width="591" height="451" alt="Tela de intimações com sugestão de prazo" src="https://github.com/user-attachments/assets/ef9a4b6f-1e7e-4fa8-842b-719065310522" />

### Celular
<img width="1038" height="677" alt="Telas do sistema no celular" src="https://github.com/user-attachments/assets/3adf5c54-5640-4441-b5f5-6db44a110dcc" />

</div>

---

## Como foi construído com IA

O código foi escrito com **Claude Code**. O meu trabalho foi definir o produto, orquestrar o agente e validar cada entrega:

1. **Especificação primeiro.** Levantei as regras com a advogada e escrevi uma especificação de negócio, que virou a fonte da verdade do agente. As telas foram prototipadas no Claude Design antes de qualquer código.
2. **Regras para o agente.** Um `CLAUDE.md` fixa o que não se negocia (autorização sempre no servidor, LGPD, "o sistema nunca cria prazo sozinho") e as convenções do código. Tudo o que a regra não cobre o agente para e pergunta.
3. **Construção em fases.** Foram 8 fases (fundação, cadastros, agenda, calendário forense, intimações, documentos, financeiro e celular). Cada fase só começava com a anterior testada.
4. **Validação.** Cada fase passava por testes automatizados, revisão de permissões, conferência lado a lado com o protótipo (no computador e no celular) e um roteiro de teste manual.

**Em números:** cerca de 250 commits entre 9 e 28 de outubro de 2026, 78 arquivos de teste e CI em todo push.

## Decisões de que me orgulho

- **Permissões testadas por matriz.** Cada rota da API é testada contra todos os perfis, e uma rota nova sem linha na matriz derruba o CI.
- **Regras críticas também no banco.** A divisão de honorários tem que somar 100%, e isso é garantido por trigger no banco, não só pela tela. Um estorno é sempre um lançamento novo, nunca a edição do anterior.
- **IA onde é seguro, regra onde precisa ser exato.** O cálculo de prazo é uma função determinística, sem modelo de linguagem, porque prazo fatal não admite "provavelmente". Mesmo assim, a sugestão segue desligada em produção até ser validada com 20 prazos reais.
- **LGPD de verdade.** Os dados e arquivos ficam no Brasil, em bucket privado com links temporários. Os logs são redigidos, sem CPF, número de processo ou texto de intimação. Há auditoria só de inserção para as ações sensíveis.

## Stack

| Parte | Tecnologias |
|---|---|
| Frontend | React, Vite, TypeScript, Tailwind, shadcn/ui, TanStack Query, React Hook Form + Zod |
| Backend | Node, TypeScript, Fastify, Prisma, Better Auth (2FA TOTP obrigatório), docxtemplater |
| Dados | PostgreSQL (Supabase, São Paulo), Google Cloud Storage (São Paulo) |
| Infra | Cloud Run e Firebase Hosting no Brasil, Cloud Scheduler para a captura, Resend para e-mail |
| Qualidade | Vitest, GitHub Actions (lint, typecheck, testes e build em todo push) |

---

## Código-fonte e acesso

> O sistema guarda dados reais de clientes. Por isso o código-fonte é privado e o acesso ao sistema é restrito ao escritório. Este repositório documenta o produto e a arquitetura. Posso mostrar uma demonstração com dados fictícios mediante pedido.
