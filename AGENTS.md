# AGENTS.md — Hiring & Ramp OS

## Missão do produto
Construir e validar um SaaS B2B em PT-BR para PMEs que precisam contratar profissionais comerciais e levá-los até produtividade. Não é ATS genérico nem ERP de RH.

Objeto central: **Perfil de Sucesso**.

Jornada-alvo:
Necessidade do negócio → Perfil de Sucesso → Kit de Recrutamento → Vaga pública → Candidatos → Evidências/Avaliação humana → Contratação → Plano 30/60/90 → Check-ins → Ramp Score → Contribuição da contratação.

Beachhead da V1: contratações comerciais B2B, especialmente BDR/SDR/pré-vendas e vendedor consultivo, para empresas de tecnologia, engenharia, segurança eletrônica, serviços técnicos e negócios B2B semelhantes.

## Regra financeira do projeto
**ZERO upgrade pago sem autorização explícita do dono do projeto.**
- Lovable: somente plano gratuito e créditos gratuitos.
- GitHub: somente recursos do plano gratuito.
- Não habilitar serviços pagos, add-ons, top-ups, domínio pago, Copilot, Codespaces pago ou APIs pagas.
- Se uma tarefa exigir gasto, parar e reportar antes.

## Princípios de produto
1. Funcionalidade > clareza > UX > estética.
2. Nenhum botão falso ou integração fictícia.
3. IA nunca decide contratação.
4. Não mostrar “fit %”, probabilidade de sucesso ou reprovação automática.
5. Avaliações são humanas; matemática apenas consolida notas explicitamente dadas por avaliadores.
6. Se uma regra determinística resolver, prefira-a à IA.
7. Não inventar metas, benchmarks ou fatos ausentes.
8. Inputs do gestor devem ser transformados em conteúdo profissional; não apenas concatenados.
9. Diferenciar: segmento_empresa, icp_alvo, produto_servico e funcao/cargo.
10. Dados de candidatos nunca podem atravessar organizações; preservar RLS/multi-tenant.

## Competência → Evidência
- Persistência → pergunta comportamental
- Comunicação → entrevista/simulação
- Organização → cenário/teste
- Raciocínio comercial → teste prático
- Prospecção → teste prático
- Aprendizado → tarefa com instrução nova + execução

## Ramp Score
Determinístico.
- dias 1–7: Capacidade 60%, Execução 30%, Resultado 10%
- dias 8–30: 35% / 40% / 25%
- dias 31–60: 20% / 35% / 45%
- dias 61–90: 10% / 30% / 60%

Score = C*pC + E*pE + R*pR
- 85–100: No ritmo esperado
- 70–84: Atenção
- <70: Precisa de intervenção

Nunca sugerir demissão automaticamente. Diagnosticar divergência entre esperado e realizado.

## UX
- PT-BR.
- SaaS B2B limpo, sério, contemporâneo.
- Fundo claro, navegação simples.
- Sem gradientes, glassmorphism, excesso de cards ou animações.
- Desktop para gestão; vaga pública mobile-first.
- Não copiar a identidade da Magistral; produto terá marca própria depois.

## Testes obrigatórios antes de considerar tarefa concluída
Sempre que alterar código:
1. instalar dependências somente por meios gratuitos já previstos no projeto;
2. rodar typecheck;
3. rodar lint/build se configurados;
4. testar as rotas afetadas;
5. quando houver ambiente executável, usar navegador/Playwright para testar fluxo real;
6. checar console e erros de rede;
7. testar persistência após refresh;
8. testar estados vazio/loading/erro/sucesso;
9. testar mobile quando a mudança afetar vaga pública/formulários;
10. corrigir falhas encontradas e repetir os testes.

Nunca delegar ao usuário testes técnicos básicos que o agente consiga executar. O usuário deve validar decisões de produto/copy, não descobrir regressões de código.

## Fluxo de QA prioritário
Quando credenciais/ambiente de teste estiverem disponíveis, automatizar:
1. criar/entrar em organização de teste;
2. Nova contratação;
3. preencher necessidade B2B;
4. gerar, editar e salvar Perfil de Sucesso;
5. criar Kit;
6. publicar vaga;
7. abrir página pública;
8. enviar candidatura fictícia;
9. confirmar candidatura no painel;
10. abrir ficha;
11. registrar evidências e scorecard humano;
12. mover candidato entre etapas;
13. refresh e confirmar persistência;
14. contratar;
15. iniciar plano 30/60/90;
16. registrar check-in;
17. verificar Ramp Score.

## Regras de segurança
- Não relaxar RLS para `true` para contornar bug.
- Toda função SECURITY DEFINER deve validar `auth.uid()`, fixar `search_path` e não aceitar user_id arbitrário do cliente.
- Inserção pública de candidatura só em vaga publicada.
- Manter aviso de privacidade e ciência antes da candidatura.
- Não inferir atributos pessoais irrelevantes de candidatos.

## Escopo fora da V1
Não construir agora: folha de pagamento, ponto, férias, benefícios, DISC/testes psicológicos proprietários, marketplace de vagas, Meta Ads API, LinkedIn API, WhatsApp API, LMS completo, payroll ou ERP de RH.

## Método de trabalho para Codex
- Ler este arquivo e `CODEX_HANDOFF.md` antes de editar.
- Trabalhar em branches pequenas.
- Preferir PRs pequenos com descrição do que foi alterado e como foi testado.
- Não fazer refatoração ampla sem necessidade.
- Corrigir regressões antes de adicionar novas features.
- Quando houver dúvida de produto que não possa ser resolvida por código/teste, registrar claramente e pedir decisão humana.
