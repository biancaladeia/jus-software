# jus-software

Plataforma full-stack de gestão operacional e inteligência jurídica concebida para centralizar, automatizar e otimizar fluxos de trabalho em escritórios de advocacia.

---

## Visão Geral

O **`jus-software`** é uma solução de software orientada a processos que substitui a fragmentação de ferramentas operacionais por uma arquitetura unificada. Projetado com uma responsividade total para desktope mobile, o sistema integra o acompanhamento automático de publicações dos tribunais, a extração preditiva de prazos, a geração parametrizada de documentos e o controlo financeiro avançado com divisão proporcional de honorários.

---

## Tech Stack & Arquitetura

* **Frontend & Mobile:** React / TypeScript, Tailwind CSS, componentes responsivos otimizados para ecrã inteiro e dispositivos móveis (PWA/Web).
* **Backend & Cloud:** Python, Node.js, Supabase (PostgreSQL relacional), Vercel, Resend (envios transacionais), GCP.
* **Inteligência & Automação:** Leitura e parsing de publicações (DJEN), algoritmo de cálculo de prazos com calendário de dias úteis/feriados e integração de APIs de linguagem.
* **Segurança:** Autenticação forte com segundo fator (2FA / TOTP), gestão de tokens de recuperação, controlo de acessos por papel (RBAC) e suporte a múltiplas OABs.

---

## Módulos do Sistema

### 1. Painel de Controlo & Gestão de Prazos
* Dashboard executivo com métricas de processos ativos, casos, audiências e priorização de prazos fatais.
* Leitura em tempo real de tarefas pendentes, compromissos agendados e alertas de urgência.

### 2. Triagem e Processamento de Intimações (DJEN)
* Captura diária automatizada de publicações de múltiplas inscrições OAB.
* Análise do texto de despachos e sugestão preditiva de prazos fatais com contagem automática de dias úteis e consideração de feriados.
* Fluxo de vinculação rápida de intimações a processos e arquivamento de publicações ignoradas.

### 3. Automação de Documentos & Modelos
* Engine de geração dinâmica de minutas contratuais, procurações e declarações de hipossuficiência.
* Mapeamento automático de marcadores e preenchimento com dados extraídos da ficha do cliente e do processo.

### 4. Controlo Financeiro & Split de Honorários
* Módulo financeiro completo para registo de honorários iniciais, êxito, sucumbência e serviços avulsos.
* Aplicação automática de regras de *split* de receitas e divisão de honorários entre sócios e parceiros externos.
* Visão consolidada de valores a receber, recebidos e lançamentos em atraso.

### 5. Navegação & Experiência Multi-Dispositivo
* Interface Desktop com painéis laterais (gavetas) e fluxos contextuais sem perda de navegação.
* Aplicação móvel com suporte a captura de documentos via câmara, verificação de notificações e gestão completa em mobilidade.

---

## 🔒 Nota de Privacidade & Código-Fonte

> O código-fonte deste repositório é mantido sob propriedade confidencial e acesso restrito por motivos de conformidade com a LGPD e segredo de negócio. Este repositório serve como especificação técnica e documentação de arquitetura do produto em produção.
