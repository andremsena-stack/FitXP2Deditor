# Changelog — FitXP2D Editor (regras do GEM)

Formato: data · o que mudou. Suba o campo `version` do JSON quando mexer em coordenadas.

## 2026-06-13 — v1.11 (resumo 'Regras de Ouro' no topo)
- Adicionado bloco TL;DR com as 9 regras críticas no topo do GEM-INSTRUCTIONS (fundo verde/alpha, canvas/pose, cel-shading/contorno, módulo+âncoras+rosto liso, item+nome+seed, portes, mesma-seed cross-gênero, muscle fem wellness/Mewtwo, folha). Consolidação p/ o Gem reler e re-sincronizar. Sem mudança de coordenadas.

## 2026-06-13 — v1.10 (DNA do muscle feminino: silhueta Mewtwo/wellness)
- Refinado com referência aprovada (só proporção; estética anime/olhos/cabelo/3-4 descartada). §10 muscle feminino: massa cresce na PARTE DE BAIXO + core (coxas/glúteos/panturrilhas/abdômen/quadril), tronco superior CONTIDO (ombro ~nível fit), cintura marcada. Proibido V-taper masculino. Silhueta-alvo 'Mewtwo': base poderosa, topo enxuto.

## 2026-06-13 — v1.9 (muscle feminino = wellness, não masculino)
- §10: muscle por gênero. Feminino = WELLNESS/atlético mantendo silhueta feminina (cintura/quadril, ombros não-masculinos); proibido trapézio/peitoral/ombros de fisiculturista masculino. (Motivo: muscle fem saindo masculinizado.)

## 2026-06-13 — v1.8 (gêneros análogos = mesma seed)
- Problema: feminino divergindo do masculino no estilo. §10.5: ao gerar o gênero OPOSTO de um set aprovado, reutilizar a SEED EXATA do set aprovado + mesma referência (trava o traço/sombreado entre masc e fem; só a anatomia muda).

## 2026-06-13 — v1.7 (lastro por-célula + separação limpa)
- §4B: cada célula = 1 corpo centrado no SEU eixo de torso (lastro por-célula); separação só pelo MESMO fundo (sem divisores/linhas de cor — nem verde-escuro nem branco); todos os corpos da folha com cabeça/esqueleto idênticos (só largura muda).
- (Cutter: keyer de verde ampliado p/ remover verde claro E escuro = divisores; registro ancora o eixo do torso por célula.)

## 2026-06-13 — v1.6 (consistência de detalhe entre peças)
- Problema: peças saindo com níveis de detalhe diferentes (gerações/seeds/resoluções distintas).
- Nova §10.5: slim/fit/muscle diferem em MASSA não em detalhe; mesmo vocabulário muscular (sem veias/estrias); gerar o SET inteiro numa folha com MESMA seed; todos os sets na MESMA ref de estilo; mesmo contorno/nº de tons/resolução efetiva.

## 2026-06-13 — v1.5 (imagem tem prioridade sobre o manifesto)
- O motor do Gemini não entrega imagem+texto juntos. Regra §4B: **entregar a IMAGEM**; manifesto é OPCIONAL (o Claude controla nomes e fatia pela proporção). Manifesto, se vier, em mensagem separada. Células quadradas.
- (Lado Claude: `cut_sheet.py` agora corta folha SEM manifesto via `--cols/--rows/--names`.)

## 2026-06-13 — v1.4 (fallback de corte: chroma verde)
- Evidência: o NBP segue entregando **xadrez pintado + marca d'água** (não alpha real),
  e o xadrez é impossível de recortar limpo. Regra de fundo revista: **alpha real preferido;
  se não der, fundo SÓLIDO CHAPADO verde-croma #00FF00** (uniforme, sem padrão/gradiente/
  marca) — recortável por chroma. Proibido SEMPRE: xadrez, gradiente, marca d'água, e cor de
  fundo próxima das do sprite (sem magenta/roxo). Regras renumeradas.

## 2026-06-13 — v1.3 (correções pós-auditoria do Gemini)
Gemini relatou entendimento com 5 desvios; corrigidos/blindados:
- **CHIBI ≠ LPC 64×64** (Gemini achava que era grid LPC) — nota explícita + removida a
  menção a "anchors_master.json do LPC" no `chibi-anchors.json` que o confundia.
- **LESSCHIBI = ~5 cabeças** (Gemini disse 6–7) — explicitado "NÃO 6–7".
- **Contorno #1A1420** (Gemini usou #1A0B2E) e **~8px@1024 ≈2px@256, NÃO 1px** (Gemini usou 1px).
- **Fundo:** proibido magenta/chroma-key #FF00FF (Gemini introduziu) — só alpha real.
- **AA:** permitido leve no contorno/bandas (alvo = refs chibi suaves), NÃO retro 8-bit sem AA
  (Gemini proibiu AA total). Luz **simétrica de cima-frente** (Gemini usou canto sup. esquerdo).
- Adicionada regra **calota/vazado** (peça opaca só na própria área; resto transparente).

## 2026-06-13 — v1.2 (consolida o prompt antigo)
- Comparado com o prompt single-shot antigo: tudo dele migrado/melhorado. Adições:
  nota de que SUBSTITUI o prompt antigo; **estética 16-bit (SNES)** explícita;
  **esclarecimento de largura de ombro** (ombro ≥ cabeça, V-taper slim→muscle; sem ombros
  70%). Coordenadas/specs inalteradas (já eram o spec aprovado).

## 2026-06-13 — v1.1 (instruções detalhadas)
- `GEM-INSTRUCTIONS.md` muito mais específico: **px @1024²** por âncora (chibi e lesschibi),
  contorno (#1A1420, ~8px), cel-shading 3 tons + direção de luz, **paleta com hex** (roxo
  #9118D6/#5E0E8B/#B57BE8, grafite #2B2B33, gelo #F4F4F0, rampa de pele neutra),
  **pose/membros** (braços com vão p/ camada), **olhos-vazios** exato, regras de recolor,
  tabela de **diferenças entre módulos** e **checklist de auto-verificação**.
- Coordenadas (specs JSON) inalteradas.

## 2026-06-13 — v1 (inicial)
- Estrutura do repo + auto-atualização do GEM via raw URLs (`GEM-BOOTSTRAP.md`).
- `GEM-INSTRUCTIONS.md`: regras de saída (alpha real, sem xadrez/marca d'água, canvas
  fixo 1024² por módulo), modo ITEM isolado, formato de corte (ITEM e SHEET+manifesto),
  paper-doll por slot (corpo/olhos/cabelo/top/bottom/tênis/óculos) p/ **CHIBI e LESSCHIBI**.
- `specs/chibi-anchors.json` v1 (cabeça ~⅓; olhos 18%, queixo 36%, ombros 41%, quadril
  60%, pés 96%; ombro slim96/fit112/muscle132 px@256).
- `specs/lesschibi-anchors.json` v1 (cabeça ~⅕; olhos 14%, queixo 24%, ombros 30%,
  cintura 46%, quadril 53%, joelhos 74%, pés 96%; ombro slim82/fit98/muscle118 px@256).
- `specs/sheet-manifest.schema.json` (corte determinístico de folhas/spritesheets).
- Decisão: olhos VAZIOS nos dois módulos (camada modular). Revisar se quiser rosto baked
  no lesschibi.
