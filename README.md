# AI System Validation Ontology

Ontologia de fundamentação (OntoUML/UFO) para validação ética e de conformidade de sistemas de IA generativa — projeto de mestrado.

## Estrutura

- `diagrams/` — diagrama inicial da ontologia (OntoUML), imagem exportada do modelo.
- `model/` — exportações do modelo:
  - `AI System Ethics Validation Ontology.json` — exportação JSON (OntoUML Schema, via ontouml-js/OLED ou ferramenta equivalente).
  - `AI System Ethics Validation Ontology.ttl` — exportação em gUFO (OWL/Turtle), gerada a partir do modelo OntoUML.
- `docs/` — documentação complementar (glossário, decisões de modelagem, etc.).

## Documentação

- [ORSD — Documento de Especificação de Requisitos](https://docs.google.com/document/d/1ffh350ql3VRR-RyRwtUG0XIKUOtVKItY-1K3-VgVsHA/edit?usp=sharing): objetivo, escopo, usuários finais, casos de uso, requisitos funcionais (questões de competência CQ1–CQ6), requisitos não funcionais (RNF1–RNF3) e pré-glossário de termos que fundamentam esta ontologia.

## Sobre o modelo

Ontologia baseada em UFO (Unified Foundational Ontology), modelando conceitos como Nível de Risco, Instrumento Normativo, Domínio, Critério Ético, Avaliação de Conformidade, Ator (Desenvolvedor, Engenheiro de Software, Órgão Regulador) e Software Gerado por IA (em conformidade / em violação).

## gUFO

O modelo OntoUML é exportado para OWL alinhado ao [gUFO](https://nemo-ufes.github.io/gufo/) (versão leve e operacional da UFO em OWL), em `model/AI System Ethics Validation Ontology.ttl`.

Mapeamento dos estereótipos OntoUML usados para os tipos gUFO:

| Estereótipo OntoUML | Tipo gUFO | Conceitos do modelo |
| --- | --- | --- |
| Kind | `gufo:Kind` (subClassOf `gufo:FunctionalComplex`) | IA Generativa, Critério Ético, Avaliação de Conformidade, Nível de Risco, Domínio, Ator, Instrumento Normativo |
| SubKind | `gufo:SubKind` | Software Gerado por IA, Framework, Legislação |
| Phase | `gufo:Phase` | Em Conformidade, Em Violação (fases de Software Gerado por IA) |
| Role | `gufo:Role` | Desenvolvedor, Engenheiro de Software, Órgão Regulador (papéis de Ator) |
| Relator | `gufo:Relator` | Avaliação de Conformidade |
| Mode | `gufo:IntrinsicMode` | Nível de Risco |

Relações materiais e de mediação do diagrama (ex.: `atorHasCritriotico`, `atorHasSoftwareGeradoPorIa`) são exportadas como `owl:ObjectProperty` tipadas com `gufo:MaterialRelationshipType`, preservando a semântica de relação derivada (material) da UFO.

> Nota: a exportação atual do `.ttl` está com labels em `rdfs:label` sem acentuação correta (problema de codificação na exportação da ferramenta); os nomes internos (IRIs) também tiveram acentos removidos. A correção deve ser feita em uma nova exportação do modelo.

## JSON (OntoUML Schema)

`model/AI System Ethics Validation Ontology.json` é a exportação nativa do modelo no formato [ontouml-schema](https://github.com/OntoUML/ontouml-schema), usado pelo OntoUML Plugin / ontouml-js para representar o projeto de forma estruturada e independente de ferramenta.

Estrutura do arquivo:

- `Project` (raiz): `id`, `name`, `description`, `type`, `model`, `diagrams`.
- `model`: `Package` contendo `contents`, a lista de elementos do diagrama — classes (`Class`) com seus estereótipos (`kind`, `subkind`, `phase`, `role`, `relator`, `mode`, etc.), generalizações, relações e generalization sets.
- `diagrams`: representação visual (posição, forma e estilo dos elementos), usada para reconstruir o diagrama na ferramenta de modelagem.

Esse JSON é a fonte de verdade estrutural do modelo — a partir dele são gerados tanto o diagrama (`diagrams/`) quanto a exportação gUFO (`.ttl`).

> Nota: mesmo problema de codificação do `.ttl` está presente aqui — termos acentuados (ex. "Critério Ético", "Domínio") vêm com bytes corrompidos no JSON exportado. Recomenda-se reexportar o modelo garantindo UTF-8.

## Ferramentas

- Modelagem: OntoUML (Visual Paradigm / OntoUML Plugin).
- Exportação para gUFO: ontouml-js ou OLED.
