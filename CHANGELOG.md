# Changelog — FitXP2D Editor (regras do GEM)

Formato: data · o que mudou. Suba o campo `version` do JSON quando mexer em coordenadas.

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
