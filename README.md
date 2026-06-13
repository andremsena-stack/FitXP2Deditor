# FitXP2D Editor — regras vivas do GEM (NBP/Gemini)

Repositório **fonte da verdade** para o GEM "Editor 2D" do Gemini que gera os assets de
avatar do app **FITXP** (estilos **CHIBI** e **LESSCHIBI**, sistema **paper-doll**).
A ideia: o GEM **puxa as regras daqui** a cada tarefa; refinamos editando estes arquivos
(commit) e o GEM passa a obedecer à versão nova **sem reconfiguração manual**.

## Conteúdo
| Arquivo | O quê |
|---|---|
| `GEM-INSTRUCTIONS.md` | **Instruções-mestre** do GEM (regras de saída, paper-doll por slot, specs dos 2 módulos, modo item, formato de corte). |
| `GEM-BOOTSTRAP.md` | Texto curto p/ colar nas *Instructions* do Gem no Gemini — manda o GEM ler as regras deste repo. |
| `specs/chibi-anchors.json` | Coordenadas/âncoras do módulo CHIBI (caixa 256², cabeça ~⅓). |
| `specs/lesschibi-anchors.json` | Coordenadas/âncoras do módulo LESSCHIBI (semi-realista, cabeça ~⅕). |
| `specs/sheet-manifest.schema.json` | Schema do **manifesto de corte** que acompanha folhas (sheets) com vários itens/frames. |
| `CHANGELOG.md` | Histórico de refinamentos. |

## Como o GEM consome (auto-atualização)
O Gem do Gemini lê as regras via **URL context** nas raw URLs (branch `main`), ex.:
`https://raw.githubusercontent.com/andremsena-stack/FitXP2Deditor/main/GEM-INSTRUCTIONS.md`
Cole o `GEM-BOOTSTRAP.md` nas instruções do Gem **uma vez**; depois é só editar este repo.

## Fluxo de produção
1. NBP gera **PNG com alpha real** (sem xadrez, sem marca d'água), canvas fixo, ancorado.
2. Itens isolados (1 PNG) ou **sheets** + `manifest.json` (corte determinístico).
3. **Claude** recorta/normaliza p/ a caixa do app (256²) e aplica no FITXP.

## Pipeline de corte (lado Claude / app)
O app FITXP vive em outro repositório. Lá, o pipeline lê estes specs + o manifesto e
fatia/normaliza cada célula para `public/avatar/<chibi|lesschibi>/<slot>/…png`.
Mantemos cópias dos specs em ambos os lados; **este repo é o canônico para a GERAÇÃO**.

## Como refinar
Edite o arquivo, suba o `version` do JSON quando mudar coordenadas, registre no
`CHANGELOG.md`, faça commit/push. O GEM pega a versão nova na próxima tarefa.
