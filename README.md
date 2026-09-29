# AI System Validation Ontology

Ontologia de fundamentação (OntoUML/UFO) para validação ética e de conformidade de sistemas de IA generativa — projeto de mestrado.

![AI System Validation Ontology (v5)](<diagrams/AI System Validation Ontology-v5.jpg>)

## Estrutura

- `diagrams/` — diagrama principal da ontologia (OntoUML, v5), imagem exportada do modelo.
- `model/` — exportações do modelo:
  - `AI System Ethics Validation Ontology.json` — exportação JSON (OntoUML Schema, via ontouml-js/OLED ou ferramenta equivalente).
  - `AI System Ethics Validation Ontology.ttl` — exportação em gUFO (OWL/Turtle), gerada a partir do modelo OntoUML.
- `docs/` — documentação complementar (glossário, decisões de modelagem, etc.).

## Documentação

- [ORSD — Documento de Especificação de Requisitos](https://docs.google.com/document/d/1ffh350ql3VRR-RyRwtUG0XIKUOtVKItY-1K3-VgVsHA/edit?usp=sharing): objetivo, escopo, usuários finais, casos de uso, requisitos funcionais (questões de competência CQ1–CQ6), requisitos não funcionais (RNF1–RNF3) e pré-glossário de termos que fundamentam esta ontologia.

## Sobre o modelo

Ontologia baseada em UFO (Unified Foundational Ontology). Principais conceitos da versão atual (v5):

- **IA Generativa** — participa da **Geração de Software** (evento), que cria o **Software Gerado por IA**.
- **Software Gerado por IA** — particionado nas fases **Em Conformidade** / **Em Violação** (generalization set disjunto e completo).
- **Nível de Risco** — qualidade que caracteriza a IA Generativa, especializada em **Crítico**, **Alto**, **Médio** e **Baixo** (completo).
- **Instrumento Normativo** — particionado em **Legislação** e **Framework** (disjunto e completo); estabelece **Critérios Éticos**.
- **Critério Ético** — do qual o **Domínio** depende externamente (relação *Aplica-se*).
- **Agente Avaliador** — categoria particionada em **Profissional** e **Organização** (disjunto e completo):
  - Profissional: papéis **Desenvolvedor de Software**, **Engenheiro de Software**, **Analista de Qualidade**.
  - Organização: papéis **Órgão Regulador**, **Comitê de Ética**, **Time de Governança**.
- **Avaliação de Conformidade** — relator que media Agente Avaliador, IA Generativa e Software Gerado por IA.
- **Ato Normativo** — relator que media Critério Ético e Instrumento Normativo.

## gUFO

O modelo OntoUML é exportado para OWL alinhado ao [gUFO](https://nemo-ufes.github.io/gufo/) (versão leve e operacional da UFO em OWL), em `model/AI System Ethics Validation Ontology.ttl`.

Mapeamento dos estereótipos OntoUML usados para os tipos gUFO:

| Estereótipo OntoUML | Tipo gUFO | Conceitos do modelo |
| --- | --- | --- |
| Kind | `gufo:Kind` (subClassOf `gufo:FunctionalComplex`) | IA Generativa, Software Gerado por IA, Critério Ético, Domínio, Instrumento Normativo, Profissional, Organização |
| Category | `gufo:Category` | Agente Avaliador |
| SubKind | `gufo:SubKind` | Framework, Legislação, Crítico, Alto, Médio, Baixo |
| Phase | `gufo:Phase` | Em Conformidade, Em Violação (fases de Software Gerado por IA) |
| Role | `gufo:Role` | Desenvolvedor de Software, Engenheiro de Software, Analista de Qualidade (papéis de Profissional); Órgão Regulador, Comitê de Ética, Time de Governança (papéis de Organização) |
| Relator | `gufo:Kind` (subClassOf `gufo:Relator`) | Avaliação de Conformidade, Ato Normativo |
| Quality | `gufo:Kind` (subClassOf `gufo:Quality`) | Nível de Risco |
| Event | `gufo:EventType` (subClassOf `gufo:Event`) | Geração de Software |

Relações do diagrama e sua exportação:

- **Material** (ex.: *Estabelece*, *Utiliza*) → `owl:ObjectProperty` tipada com `gufo:MaterialRelationshipType`.
- **Mediation** → restrições sobre `gufo:mediates` (ex.: Avaliação de Conformidade media Software Gerado por IA e IA Generativa; Ato Normativo media Critério Ético e Instrumento Normativo).
- **Characterization** → restrições sobre `gufo:inheresIn` (Nível de Risco inere em IA Generativa).
- **External dependence** → restrição sobre `gufo:externallyDependsOn` (Domínio → Critério Ético).
- **Participation** / **Creation** → restrições sobre `gufo:participatedIn` e `gufo:wasCreatedIn` (IA Generativa participa da Geração de Software, que cria o Software Gerado por IA).
- **Generalization sets** disjuntos/completos → `owl:AllDisjointClasses` e `owl:equivalentClass` com `owl:unionOf`.

> Nota: o arquivo está em UTF-8. A exportação original da ferramenta perdia os acentos dos `rdfs:label`; eles foram restaurados a partir dos nomes das classes no JSON. Os nomes internos (IRIs) seguem sem acentos (ex. `:Critriotico`, `:NvelDeRisco`), como gerados pela exportação.

## JSON (OntoUML Schema)

`model/AI System Ethics Validation Ontology.json` é a exportação nativa do modelo no formato [ontouml-schema](https://github.com/OntoUML/ontouml-schema), usado pelo OntoUML Plugin / ontouml-js para representar o projeto de forma estruturada e independente de ferramenta.

Estrutura do arquivo:

- `Project` (raiz): `id`, `name`, `description`, `type`, `model`, `diagrams`.
- `model`: `Package` contendo `contents`, a lista de elementos do diagrama — classes (`Class`) com seus estereótipos (`kind`, `subkind`, `phase`, `role`, `relator`, `category`, `quality`, `event`, etc.), generalizações, relações e generalization sets.
- `diagrams`: representação visual (posição, forma e estilo dos elementos), usada para reconstruir o diagrama na ferramenta de modelagem.

Esse JSON é a fonte de verdade estrutural do modelo — a partir dele são gerados tanto o diagrama (`diagrams/`) quanto a exportação gUFO (`.ttl`).

> Nota: a ferramenta exporta o JSON em Windows-1252; o arquivo do repositório foi convertido para UTF-8. Ao reexportar o modelo, repetir a conversão.

## Ferramentas

- Modelagem: OntoUML (Visual Paradigm / OntoUML Plugin).
- Exportação para gUFO: ontouml-js ou OLED.
