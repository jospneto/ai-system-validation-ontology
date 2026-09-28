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

## Ferramentas

- Modelagem: OntoUML (Visual Paradigm / OntoUML Plugin).
- Exportação para gUFO: ontouml-js ou OLED.
