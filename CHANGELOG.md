# Changelog — FitXP2D Editor (regras do GEM)

Formato: data · o que mudou. Suba o campo `version` do JSON quando mexer em coordenadas.

## 2026-06-15 — v1.18 (coordenadas medidas nos prompts)
- **§9 (olhos/cabelo):** prompts ganharam as coordenadas reais @256 (medidas dos assets aprovados + .pxo do usuário) p/ acertar o encaixe na geração: cabeça coroa **y10**, **orelha-a-orelha x92–162 (71px)** em y52–60, queixo ~y82; **olhos masc y48–61 (cy54, descidos 3px sob a franja) / fem y45–58 (cy51)**, par ~47px centro x127; cabelo cobre x92–162 (1.0–1.24× cabeça), coroa y1–10, centro x127.
- **§9 cabelo PixelLab:** documentada a alternativa **alpha real** (PixelLab) ao template ciano — só cabelo em fundo transparente; o Claude reescala (modo `--transparent`: largura 1.24× orelha = ~88px, coroa y1). Sem mudança nas coordenadas dos JSON.
- (Lado Claude: `place_hair.py` ganhou `--transparent`; olhos masc re-ancorados +3px no app; `AI-STUDIO-SYSTEM-INSTRUCTIONS.md` espelhado.)

## 2026-06-15 — v1.19 (§14 otimização de geração PixelLab)
- **§14 (novo):** consolidou as regras aprendidas na produção em massa via PixelLab: (1) contorno-guia CIANO #18CAB5 2px — REMOVIDO no corte, não recolorido (não engrossa outline); (2) VAZADO/hollow nas aberturas (gola/cavas/pernas/faixa-olhos) — nunca face interna; (3) tamanho 1:1 com o corpo anexado (cabelo=cabeça ~71px, não encher canvas; roupa=silhueta do porte); (4) roupa BUILD-AWARE `<slot>-<gen>-<porte>-<família>`; (5) TRAJE full-body (ninja/samurai/tsunade), exclusivo muscle, esconde slots cobertos; (6) sem " (cópia)" no nome. Sem mudança nas coordenadas dos JSON.
- (Lado Claude/app: avatar CHIBI v2 virou o ATUAL — compositor `ChibiAvatar` + editor `ChibiCreator` + manifesto `chibi-pack.generated.ts` + slot `traje` + gating por porte/premium. Tools de corte: `place_hair.py` (--transparent/--decyan), `place_clothing.py`, `build_chibi_manifest.py`. Doc de integração: AVATAR-GAMIFICATION-ARCHITECTURE.md §5.V2.)

## 2026-06-15 — v1.17 (cabelo longo: silhueta do corpo, sem "fundo")
- **§9 cabelo:** cabelo é compartilhado entre slim/fit/muscle (larguras diferentes). Abaixo do
  pescoço/queixo o cabelo DEVE acompanhar a silhueta do corpo ciano (mechas coladas ao contorno,
  mesma largura) OU não descer (parar no ombro). PROIBIDO: cabelo abaixo do pescoço fora do corpo
  ciano (sobre o fundo magenta) ou cortina cheia cobrindo o tronco — vira erro de corte (massa
  interna cobre o tronco ou mechas flutuam sobre o fundo). Resumo: abaixo do pescoço, cabelo só
  onde há corpo por baixo, justo à silhueta.
- (Lado Claude: a camada `-tras` é recortada ao **alfa do corpo renderizado + borda ~5px** no
  momento da composição = clip dinâmico por porte; 1 asset serve os 3 portes. Documentado em
  `chibi-anchors.json` slot hair `long_hair_clip`. Ancoragem do cabelo passou a ser pela CAVIDADE
  do rosto, e cada estilo vira 2 camadas `-frente`/`-tras` cortadas no queixo.)

## 2026-06-14 — v1.16 (cabelo: preservar o corpo ciano do template)
- **§9 cabelo:** o GEM deve devolver o **corpo/cabeça CIANO IDÊNTICO ao template** (mesma escala/posição) — desenhar SÓ o cabelo por cima. Motivo: o lado Claude registra o cabelo pela **cabeça ciana** (linha das bochechas/orelhas, visível sob o cabelo) e mapeia p/ a cabeça real do corpo; se o GEM encolhe/move o corpo ciano (visto no "espetado", ~30% menor), o encaixe vira trabalho manual. Sem mudança de coordenadas.
- (Lado Claude: `place_hair.py` reescrito — registro pela bochecha ciana → bochecha do corpo, com `--scale`/`--dy` de ajuste fino; params aprovados curto/espetado/bagunçado/longo travados. Substitui o crown-guess que desencaixava.)

## 2026-06-14 — v1.15 (chroma por slot + módulos olhos/cabelo)
- **CHROMA POR SLOT (§1.5, novo):** o fundo de corte muda por slot porque não pode ser uma cor que o sprite contém. corpo/roupas/tênis = verde #00FF00; **olhos = magenta #FF00FF** (a íris pode ser verde); **cabelo = template CIANO** (cor de cabelo pode ser verde + evita contorno-de-rosto). Magenta #FF00FF ≠ roxo de marca #9118D6. Regra de Ouro #1 e §1 regra 3 atualizadas (a antiga proibição de magenta foi reconciliada).
- **Módulo OLHOS (§9):** overlay **sobrancelha+olho** sobre magenta, sem rosto; gênero × cor (castanho/azul/verde); folha 3×2 (masc cima/fem baixo) ou item. Ancoragem no soquete (~0.56× cabeça, canal do rosto).
- **Módulo CABELO (§9) = TEMPLATE CIANO:** usuário anexa figura ciano sobre magenta; GEM desenha SÓ o cabelo (sem rosto/olhos/orelha/contorno-de-rosto — esse contorno sujava o corte). Encaixe justo: coroa encosta no topo do crânio, linha do cabelo na testa, laterais até orelha, largura ~1.0× cabeça; volume sobe acima, longo desce sobre o corpo. 1 cabelo/imagem, cor base castanho.
- Checklist §13 atualizado p/ chroma por slot + checks de olhos/cabelo. Sem mudança nas coordenadas dos JSON.

## 2026-06-14 — v1.14 (cabeça/frame do feminino = iguais ao masculino)
- Auditoria: feminino saiu mais longilíneo (cabeça menor/estreita, corpo estreito, pernas longas). §6: TAMANHO e LARGURA da cabeça + largura-base do corpo são IGUAIS entre gêneros (não só a posição). Proibido afinar/alongar o feminino; ele só ganha cintura/quadril/busto sobre o MESMO esqueleto e MESMA cabeça do masculino.

## 2026-06-13 — v1.13 (seed canônica travada por DNA)
- Seed aprovada vira CANÔNICA do módulo, gravada em `approved_seed` do spec. CHIBI = 8712395610. Toda geração chibi (qualquer slot/gênero/porte) usa essa seed. lesschibi: approved_seed=null até aprovar o 1º set. Regra 7 e Regra de Ouro atualizadas.

## 2026-06-13 — v1.12 (proporção vertical travada cross-gênero)
- Medição mostrou masc com pernas longas (virilha ~55%) e fem com pernas curtas/tronco longo (virilha ~65%) = desconexão de escala. §6: PROPORÇÃO VERTICAL TRAVADA idêntica masc/fem (mesma cabeça, virilha 60%, joelho 80%, pés 96%); só muda largura/anatomia. Regra de ouro #10. Ao gerar gênero oposto: anexar o corpo pronto como ref de proporção + mesma seed.

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
