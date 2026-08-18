# CODEX_HANDOFF — Hiring & Ramp OS

## Estado em 18/08/2026

Projeto Lovable de origem:
- Project ID: `64d6af56-e17a-45ee-b2fd-b5a40c99b116`
- Nome atual/provisório: `Perfil em Ritmo` / `Hiring & Ramp OS`
- Lovable preview: `https://id-preview--64d6af56-e17a-45ee-b2fd-b5a40c99b116.lovable.app`
- Último commit conhecido no Lovable: `34d1b7596aaf84c8ddc5915f64a2bf22613bbe3c`
- Stack: TanStack Start + TypeScript + Tailwind/shadcn + Lovable Cloud/Supabase.

## Regra financeira
Tudo deve permanecer em recursos gratuitos por enquanto. Não habilitar recurso pago no Lovable ou GitHub. Não contratar GitHub Copilot/Codespaces pagos. Se qualquer ação exigir cobrança, pare e reporte.

## Visão do produto
Sistema de contratação até produtividade para PMEs B2B. Beachhead: comercial B2B, especialmente BDR/SDR/pré-vendas e vendedor consultivo em empresas de tecnologia, engenharia, segurança eletrônica, serviços técnicos e negócios semelhantes.

Objeto central: Perfil de Sucesso.

Fluxo:
Necessidade → Perfil de Sucesso → Kit de Recrutamento → Vaga pública → Candidatura → Candidatos → Evidências/scorecard humano → Contratação → Rampagem 30/60/90 → Check-ins → Ramp Score → Contribuição.

## O que já foi implementado no Lovable

### Conta e organização
- autenticação e isolamento por organização;
- RLS multiempresa;
- criação de organização corrigida com RPC `create_org_with_owner` para criar org + owner atomicamente;
- demo opcional.

### Nova Necessidade
Wizard em PT-BR. Campos recentes separam:
- `segmento_empresa`;
- `icp_alvo`;
- `produto_servico`;
- ticket interno;
- tipo de venda;
- meta de reuniões, se conhecida;
- cidade;
- modelo presencial/híbrido/remoto;
- estrutura comercial;
- clareza sobre a função (`funcao_certeza`) e nome quando informado (`funcao_nome`).

### Perfil de Sucesso
Geração determinística para comercial B2B. Editável e persistido.
Inclui:
- missão;
- resultados;
- responsabilidades;
- competências;
- por que cada competência importa;
- como comprovar;
- requisitos obrigatórios/desejáveis;
- indicadores Atividade/Conversão/Resultado;
- preview 30/60/90.

Regra competência → evidência implementada.

### Função/cargo
`resolveRoleTitle()` não pode transformar “Não tenho certeza” em cargo.
Quando inferido, tende a:
- prospecção/reuniões/oportunidades → `BDR / SDR B2B` internamente;
- fechamento/propostas/negociação/receita → `Vendedor consultivo B2B`.
Título público preferencial de pré-vendas: `BDR | Pré-vendas B2B`.

### Kit de recrutamento / vaga
- título/headline;
- descrição;
- copy redes;
- copy anúncio;
- WhatsApp/indicação;
- perguntas eliminatórias;
- perguntas qualificatórias;
- roteiro de entrevista;
- teste prático;
- scorecard.

Foi criado `retargetKit()` para manter título/cidade/modelo/remuneração atuais como fonte de verdade em todo o kit.
Ticket não deve vazar automaticamente para texto candidato-facing.
Sem meta conhecida, não inventar número.

### Vaga pública
- mobile-first;
- candidatura real em `applications`;
- UTM/source;
- perguntas eliminatórias estruturadas;
- perguntas qualificatórias abertas;
- privacidade/ciência obrigatória;
- proteção contra clique duplo;
- erro preserva respostas.

### Candidatos
Tela com:
- nome/e-mail;
- vaga;
- origem;
- etapa;
- data;
- próxima ação;
- filtros por vaga/etapa;
- mudança manual de etapa;
- confirmação para Contratado/Não avançou;
- `activity_log` das mudanças.

Etapas:
`Novos → Triagem → Entrevista → Teste → Finalistas → Contratado → Não avançou`

### Ficha do candidato
- contato;
- origem;
- respostas eliminatórias × qualificação;
- evidências por competência: Forte/Moderada/Fraca/Ainda não avaliada + nota humana;
- scorecard humano 1–5 com pesos;
- consolidação matemática apenas;
- histórico de etapas.

Proibido apresentar fit percentual, probabilidade de sucesso ou decisão automática.

### Rampagem
Há código/telas preliminares no projeto (`app.rampagem...`, `rampScore.ts`), mas essa parte ainda não foi validada profundamente. Não presumir que está pronta apenas porque existe no código.

## Problemas já encontrados e corrigidos
1. RLS impedia retorno da organização recém-criada antes de owner membership existir.
2. “Não tenho certeza” estava virando nome da função.
3. Cidade atual da vaga aparecia como São Paulo no topo, enquanto textos derivados ainda usavam “A definir”.
4. Inputs do wizard estavam sendo concatenados cruamente em conteúdo público.
5. ICP estava sendo confundido com segmento da empresa/candidato.
6. Perguntas eliminatórias eram textareas abertas.
7. Textos artificiais como “ramp-a” e “no-show controlado dentro do padrão do time” foram removidos.

## Próxima missão do Codex
Antes de adicionar novas features, assumir QA técnico do produto e deixar um fluxo E2E confiável.

### Fase 1 — preparar testes
1. Inspecionar `package.json`, scripts e stack.
2. Rodar instalação, typecheck, lint e build.
3. Adicionar Playwright (ou aproveitar se já existir), apenas com dependências gratuitas/open source.
4. Criar uma estratégia de testes que não dependa do proprietário manualmente a cada alteração.
5. Nunca commitar credenciais reais ou `.env` com segredos.

### Fase 2 — E2E prioritário
Com ambiente/credenciais de teste adequadas, automatizar:
1. autenticação;
2. criar/usar organização teste;
3. Nova contratação;
4. preencher necessidade;
5. gerar/editar/salvar Perfil de Sucesso;
6. criar Kit;
7. publicar vaga;
8. abrir vaga pública;
9. enviar candidatura fictícia;
10. confirmar na lista de candidatos;
11. abrir ficha;
12. registrar evidências;
13. preencher scorecard;
14. mover etapa;
15. refresh;
16. confirmar persistência e histórico.

Registrar bugs encontrados, corrigir e repetir teste.

### Fase 3 — só depois do E2E de seleção passar
Revisar/implementar de forma confiável:
- Contratar candidato → `Hire`;
- dados: início, gestor, remuneração, jornada, meta inicial, primeira avaliação;
- gerar plano 30/60/90;
- Capacidade × Execução × Resultado;
- check-in semanal curto;
- Ramp Score determinístico conforme AGENTS.md;
- diagnóstico sem sugerir demissão;
- contribuição da contratação sem inventar ROI.

## Segurança e dados
- Não quebrar RLS.
- Dados de candidatos por organização.
- Não commitar `.env` real.
- `create_org_with_owner` SECURITY DEFINER é intencional: auth.uid obrigatório, search_path fixado, sem user_id fornecido pelo cliente.
- Public application insert apenas para vaga publicada.

## Definition of Done
Uma tarefa não está concluída só porque compilou.
- typecheck limpo;
- build/lint quando aplicável;
- fluxo afetado testado;
- console/network sem erro relevante;
- refresh mantém estado persistido;
- erros/empty/loading/success tratados;
- mobile validado para páginas públicas;
- PR deve explicar exatamente o que foi testado.

## Observação sobre validação humana
O Codex deve assumir QA técnico. O proprietário deve ser acionado principalmente para decisões de produto/copy ou validação qualitativa que software não consegue decidir sozinho.
