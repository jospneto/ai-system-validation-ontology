# AI System Validation Ontology

Ontologia de fundamentação (OntoUML/UFO) para validação ética e de conformidade de sistemas de IA generativa — projeto de mestrado.

## Estrutura

- `diagrams/` — diagrama inicial da ontologia (OntoUML), imagem exportada do modelo.
- `model/` — exportações do modelo:
  - `AI System Ethics Validation Ontology.json` — exportação JSON (OntoUML Schema, via ontouml-js/OLED ou ferramenta equivalente).
  - `AI System Ethics Validation Ontology.ttl` — exportação em gUFO (OWL/Turtle), gerada a partir do modelo OntoUML.
- `docs/` — documentação complementar (glossário, decisões de modelagem, etc.).

## Sobre o modelo

Ontologia baseada em UFO (Unified Foundational Ontology), modelando conceitos como Nível de Risco, Instrumento Normativo, Domínio, Critério Ético, Avaliação de Conformidade, Ator (Desenvolvedor, Engenheiro de Software, Órgão Regulador) e Software Gerado por IA (em conformidade / em violação).

## Ferramentas

- Modelagem: OntoUML (Visual Paradigm / OntoUML Plugin).
- Exportação para gUFO: ontouml-js ou OLED.
