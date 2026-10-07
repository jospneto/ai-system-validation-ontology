# AI System Validation Ontology

Ontologia de fundamentação (OntoUML/UFO) para validação ética e de conformidade de sistemas de IA generativa — projeto de mestrado.

![AI System Validation Ontology (v8)](<diagrams/AI System Validation Ontology-v8.jpg>)

## Estrutura

- `diagrams/` — imagens exportadas do modelo (OntoUML):
  - `AI System Validation Ontology-v8.jpg` — diagrama principal (visão completa, v8).
  - `Avaliation Agent Ontology.jpg` — subdiagrama do Agente Avaliador (Profissional, Organização e seus papéis).
  - `Compliance Analysis Results Ontology.jpg` — subdiagrama do resultado da avaliação de conformidade.
  - `Domain Software Ontology.jpg` — subdiagrama dos domínios de aplicação do software gerado por IA.
  - `Ethical Criteria Ontology.jpg` — subdiagrama dos tipos de critério ético.
- `model/` — exportações do modelo:
  - `AI System Ethics Validation Ontology.json` — exportação JSON (OntoUML Schema, via ontouml-js/OLED ou ferramenta equivalente).
  - `AI System Ethics Validation Ontology.ttl` — exportação em gUFO (OWL/Turtle), gerada a partir do modelo OntoUML.
- `docs/` — documentação complementar (glossário, decisões de modelagem, etc.).

## Documentação

- [ORSD — Documento de Especificação de Requisitos](https://docs.google.com/document/d/1ffh350ql3VRR-RyRwtUG0XIKUOtVKItY-1K3-VgVsHA/edit?usp=sharing): objetivo, escopo, usuários finais, casos de uso, requisitos funcionais (questões de competência CQ1–CQ6), requisitos não funcionais (RNF1–RNF3) e pré-glossário de termos que fundamentam esta ontologia.

## Sobre o modelo

Ontologia baseada em UFO (Unified Foundational Ontology). Principais conceitos da versão atual (v8):

- **IA Generativa** — participa da **Geração de Software** (evento), que cria o **Software Gerado por IA**.
- **Software Gerado por IA** — particionado nas fases **Em Conformidade** / **Em Violação** (generalization set disjunto e completo).
- **Nível de Risco** — qualidade que caracteriza a IA Generativa, especializada em **Crítico**, **Alto**, **Médio** e **Baixo** (completo, sobreposto).
- **Instrumento Normativo** — particionado em **Legislação** e **Framework** (disjunto e completo); estabelece **Critérios Éticos**.
- **Ato Normativo** — relator que media Critério Ético e Instrumento Normativo.
- **Agente Avaliador** — categoria particionada em **Profissional** e **Organização** (disjunto e completo):
  - Profissional: papéis **Desenvolvedor de Software**, **Engenheiro de Software**, **Analista de Qualidade** (disjunto, incompleto).
  - Organização: papéis **Órgão Regulador**, **Comitê de Ética**, **Time de Governança** (disjunto, incompleto).
- **Avaliação de Conformidade** — relator central: o Agente Avaliador *realiza* a avaliação, que *avalia* o Software Gerado por IA, *utiliza* Critérios Éticos e media a IA Generativa; cada papel avaliador tem relação material com a avaliação.

![Avaliation Agent Ontology](<diagrams/Avaliation Agent Ontology.jpg>)

### Critério Ético

**Critério Ético** — particionado nos subkinds **Transparência**, **Equidade**, **Privacidade** e **Responsabilidade** (disjunto e completo).

![Ethical Criteria Ontology](<diagrams/Ethical Criteria Ontology.jpg>)

### Resultado da Conformidade

**Resultado da Conformidade** — modo (*mode*) que *deriva de* uma Avaliação de Conformidade e *valida* o Software Gerado por IA; particionado nas fases **Atendido** / **Violado** (disjunto e completo).

![Compliance Analysis Results Ontology](<diagrams/Compliance Analysis Results Ontology.jpg>)

### Domínio

**Domínio** — *roleMixin* que é componente (*componentOf*, relação *Aplica-se*) do Software Gerado por IA. Particionado (disjunto e completo) nos papéis:

- **Setorial** (kind; disjunto, incompleto): **Saúde**, **Financeiro**, **Jurídico**, **Educação**.
- **Geral** (kind): **Desenvolvimento de Software**, **Automação de Tarefas**, **Audiovisual**, **Geração de Conteúdo**.

![Domain Software Ontology](<diagrams/Domain Software Ontology.jpg>)

## gUFO

O modelo OntoUML é exportado para OWL alinhado ao [gUFO](https://nemo-ufes.github.io/gufo/) (versão leve e operacional da UFO em OWL), em `model/AI System Ethics Validation Ontology.ttl`.

Mapeamento dos estereótipos OntoUML usados para os tipos gUFO:

| Estereótipo OntoUML | Tipo gUFO | Conceitos do modelo |
| --- | --- | --- |
| Kind | `gufo:Kind` (subClassOf `gufo:FunctionalComplex`) | IA Generativa, Software Gerado por IA, Critério Ético, Instrumento Normativo, Profissional, Organização, Setorial, Geral |
| Category | `gufo:Category` | Agente Avaliador |
| RoleMixin | `gufo:RoleMixin` | Domínio |
| SubKind | `gufo:SubKind` | Framework, Legislação, Crítico, Alto, Médio, Baixo, Transparência, Equidade, Privacidade, Responsabilidade |
| Phase | `gufo:Phase` | Em Conformidade, Em Violação (fases de Software Gerado por IA); Atendido, Violado (fases de Resultado da Conformidade) |
| Role | `gufo:Role` | Desenvolvedor de Software, Engenheiro de Software, Analista de Qualidade (papéis de Profissional); Órgão Regulador, Comitê de Ética, Time de Governança (papéis de Organização); Saúde, Financeiro, Jurídico, Educação, Desenvolvimento de Software, Automação de Tarefas, Audiovisual, Geração de Conteúdo (papéis de Domínio) |
| Mode | `gufo:Kind` (subClassOf `gufo:IntrinsicMode`) | Resultado da Conformidade |
| Relator | `gufo:Kind` (subClassOf `gufo:Relator`) | Avaliação de Conformidade, Ato Normativo |
| Quality | `gufo:Kind` (subClassOf `gufo:Quality`) | Nível de Risco |
| Event | `gufo:EventType` (subClassOf `gufo:Event`) | Geração de Software |

Relações do diagrama e sua exportação:

- **Material** (ex.: *Estabelece*, *Utiliza*, *Valida*, relações entre Avaliação de Conformidade e os papéis avaliadores) → `owl:ObjectProperty` tipada com `gufo:MaterialRelationshipType`.
- **Mediation** → restrições sobre `gufo:mediates` (ex.: Avaliação de Conformidade media Software Gerado por IA, IA Generativa e Resultado da Conformidade; Agente Avaliador é mediado pela Avaliação de Conformidade; Ato Normativo media Critério Ético e Instrumento Normativo).
- **Characterization** → restrições sobre `gufo:inheresIn` (Nível de Risco inere em IA Generativa).
- **Participation** / **Creation** → restrições sobre `gufo:participatedIn` e `gufo:wasCreatedIn` (IA Generativa participa da Geração de Software, que cria o Software Gerado por IA).
- **Generalization sets** disjuntos/completos → `owl:AllDisjointClasses` e `owl:equivalentClass` com `owl:unionOf`.
- **ComponentOf** (Domínio *Aplica-se* Software Gerado por IA) não é exportada como restrição pela ferramenta; fica representada apenas no JSON/diagrama.

> Nota: o arquivo está em UTF-8. A exportação original da ferramenta perdia os acentos dos `rdfs:label`; eles foram restaurados a partir dos nomes das classes no JSON. A exportação também removia as letras acentuadas dos nomes internos (IRIs), ex. `:Critriotico`, `:ComitDetica`; eles foram corrigidos para a forma sem acento (ex. `:CriterioEtico`, `:ComiteDeEtica`, `:NivelDeRisco`). Ao reexportar, repetir as duas correções.

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
