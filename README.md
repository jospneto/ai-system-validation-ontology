# AI System Validation Ontology

Ontologia de fundamentação (OntoUML/UFO) para validação ética e de conformidade de sistemas de IA generativa — projeto de mestrado.

![AI System Validation View](<diagrams/AI System Validation View.jpg>)

## Estrutura

- `diagrams/` — views exportadas do modelo (OntoUML):
  - `AI System Validation View.jpg` — visão completa do modelo, com os padrões aplicados (SubKind, Category, Phase, Mode).
  - `Evaluation Agent View.jpg` — Agente Avaliador (*Appraiser*), Profissional, Organização e seus papéis.
  - `Ethical Criteria View.jpg` — tipos de critério ético e instrumentos normativos.
  - `Compliance Analysis Results View.jpg` — resultado da avaliação de conformidade.
  - `Domain Software View.jpg` — domínios de aplicação do software gerado por IA.
- `model/` — exportações do modelo:
  - `AI System Ethics Validation Ontology.json` — exportação JSON (OntoUML Schema, via ontouml-js/OLED ou ferramenta equivalente).
  - `AI System Ethics Validation Ontology.ttl` — exportação em gUFO (OWL/Turtle), gerada a partir do modelo OntoUML.
- `docs/` — documentação complementar:
  - `Documento de Especificação de Requisitos.pdf` — ORSD da ontologia (versão PDF).

## Documentação

- [ORSD — Documento de Especificação de Requisitos](https://docs.google.com/document/d/1ffh350ql3VRR-RyRwtUG0XIKUOtVKItY-1K3-VgVsHA/edit?usp=sharing): objetivo, escopo, usuários finais, casos de uso, requisitos funcionais (questões de competência CQ1–CQ6), requisitos não funcionais (RNF1–RNF3) e pré-glossário de termos que fundamentam esta ontologia. Versão em PDF no repositório: [`docs/Documento de Especificação de Requisitos.pdf`](<docs/Documento de Especificação de Requisitos.pdf>).

## Sobre o modelo

Ontologia baseada em UFO (Unified Foundational Ontology), com elementos nomeados em inglês. Principais conceitos:

- **Generative AI** — participa da **Software Generation** (evento), que cria o **AI-Generated Software**.
- **AI-Generated Software** — particionado nas fases **Compliant** / **Non-Compliant** (*Software-Evaluation*, disjunto e completo).
- **Risk Level** — modo que caracteriza a Generative AI, especializado em **Critical**, **High**, **Medium** e **Low** (*Defined-Risk-Level*, completo, sobreposto).
- **Compliance Assessment** — relator central: o Appraiser *performs* a avaliação, que *evaluates* o AI-Generated Software, *uses* Ethical Criteria e *classifies* a Generative AI.

### Agente Avaliador

**Appraiser** — categoria particionada em **Professional** e **Organization** (*Agent-Evaluator-Type*, disjunto e completo):

- Professional: papéis **Software Developer**, **Software Engineer**, **Quality Analyst** (disjunto, incompleto).
- Organization: papéis **Regulatory Body**, **Ethics Committee**, **Governance Team** (disjunto, incompleto).

Cada papel avaliador tem relação material com a Compliance Assessment (Relational Dependence Pattern).

![Evaluation Agent View](<diagrams/Evaluation Agent View.jpg>)

### Critério Ético

- **Ethical Criterion** — particionado nos subkinds **Transparency**, **Fairness**, **Privacy** e **Accountability** (*Ethical-Criteria-Types*, disjunto e completo).
- **Normative Instrument** — particionado em **Legislation** e **Framework** (*Normative-Instrument*, disjunto e completo); *establishes* Ethical Criteria.
- **Normative Act** — relator que media os papéis **Established Criterion** (de Ethical Criterion) e **Issuing Instrument** (de Normative Instrument).

![Ethical Criteria View](<diagrams/Ethical Criteria View.jpg>)

### Resultado da Conformidade

**Compliance Result** — modo (*mode*) que *deriva de* (*derived from*) uma Compliance Assessment e *valida* (*to validate*) o AI-Generated Software; particionado nas fases **Fulfilled** / **Violated** (*Result-Compliance*, disjunto e completo).

![Compliance Analysis Results View](<diagrams/Compliance Analysis Results View.jpg>)

### Domínio

**Domain** — *roleMixin* que é componente (*componentOf*, relação *applies*) do AI-Generated Software. Particionado (*Domain-Types*, disjunto e completo) nos papéis:

- **Industry** (kind; *Industry-Types*, disjunto, incompleto): **Healthcare**, **Financial**, **Legal**, **Education**.
- **General** (kind; *General-Types*, completo, sobreposto): **Software Development**, **Task Automation**, **Audiovisual**, **Content Generation**.

Relatores do domínio:

- **Criterion Applicability** — media Domain e **Applicable Criterion** (subkind de Ethical Criterion), que é *applicable in* um Domain.
- **Domain Application** — media Domain e **Applied Software** (subkind de AI-Generated Software), que é *applied in* um Domain.

![Domain Software View](<diagrams/Domain Software View.jpg>)

## gUFO

O modelo OntoUML é exportado para OWL alinhado ao [gUFO](https://nemo-ufes.github.io/gufo/) (versão leve e operacional da UFO em OWL), em `model/AI System Ethics Validation Ontology.ttl`.

Mapeamento dos estereótipos OntoUML usados para os tipos gUFO:

| Estereótipo OntoUML | Tipo gUFO | Conceitos do modelo |
| --- | --- | --- |
| Kind | `gufo:Kind` (subClassOf `gufo:FunctionalComplex`) | Generative AI, AI-Generated Software, Ethical Criterion, Normative Instrument, Professional, Organization, Industry, General |
| Category | `gufo:Category` | Appraiser |
| RoleMixin | `gufo:RoleMixin` | Domain |
| SubKind | `gufo:SubKind` | Framework, Legislation, Critical, High, Medium, Low, Transparency, Fairness, Privacy, Accountability, Applicable Criterion, Applied Software |
| Phase | `gufo:Phase` | Compliant, Non-Compliant (fases de AI-Generated Software); Fulfilled, Violated (fases de Compliance Result) |
| Role | `gufo:Role` | Software Developer, Software Engineer, Quality Analyst (papéis de Professional); Regulatory Body, Ethics Committee, Governance Team (papéis de Organization); Established Criterion, Issuing Instrument; Healthcare, Financial, Legal, Education, Software Development, Task Automation, Audiovisual, Content Generation (papéis de Domain) |
| Mode | `gufo:Kind` (subClassOf `gufo:IntrinsicMode`) | Compliance Result, Risk Level |
| Relator | `gufo:Kind` (subClassOf `gufo:Relator`) | Compliance Assessment, Normative Act, Criterion Applicability, Domain Application |
| Event | `gufo:EventType` (subClassOf `gufo:Event`) | Software Generation |

Relações do diagrama e sua exportação:

- **Material** (ex.: *establishes*, *uses*, *to validate*, *applicable in*, *applied in*, relações entre Compliance Assessment e os papéis avaliadores) → `owl:ObjectProperty` tipada com `gufo:MaterialRelationshipType`.
- **Mediation** → restrições sobre `gufo:mediates`.
- **Characterization** → restrições sobre `gufo:inheresIn` (Risk Level inere em Generative AI).
- **Participation** / **Creation** → restrições sobre `gufo:participatedIn` e `gufo:wasCreatedIn` (Generative AI participa da Software Generation, que cria o AI-Generated Software).
- **Generalization sets** disjuntos/completos → `owl:AllDisjointClasses` e `owl:equivalentClass` com `owl:unionOf`.
- **ComponentOf** (Domain *applies* AI-Generated Software) não é exportada como restrição pela ferramenta; fica representada apenas no JSON/diagrama.

> Nota: alguns nomes de elementos no Visual Paradigm têm TAB inicial ou quebra de linha final (ex. `"\tRisk Level"`, `"Applied Software\n"`), que a exportação leva para os `name` do JSON e os `rdfs:label` do TTL. Esses espaços foram removidos nos dois arquivos. Ao reexportar, repetir a correção ou ajustar os nomes no modelo.

## JSON (OntoUML Schema)

`model/AI System Ethics Validation Ontology.json` é a exportação nativa do modelo no formato [ontouml-schema](https://github.com/OntoUML/ontouml-schema), usado pelo OntoUML Plugin / ontouml-js para representar o projeto de forma estruturada e independente de ferramenta.

Estrutura do arquivo:

- `Project` (raiz): `id`, `name`, `description`, `type`, `model`, `diagrams`.
- `model`: `Package` contendo `contents`, a lista de elementos do diagrama — classes (`Class`) com seus estereótipos (`kind`, `subkind`, `phase`, `role`, `relator`, `category`, `mode`, `event`, etc.), generalizações, relações e generalization sets.
- `diagrams`: representação visual das 5 views (posição, forma e estilo dos elementos), usada para reconstruir os diagramas na ferramenta de modelagem.

Esse JSON é a fonte de verdade estrutural do modelo — a partir dele são gerados tanto os diagramas (`diagrams/`) quanto a exportação gUFO (`.ttl`).

## Ferramentas

- Modelagem: OntoUML (Visual Paradigm / OntoUML Plugin).
- Exportação para gUFO: ontouml-js ou OLED.
