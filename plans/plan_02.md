# Auditoría: cumplimiento de chapters/chapter_02.md frente a tasks/task_02.md

## Resumen de cumplimiento

| Requisito                                                                                | Estado                           | Observación                                                                                                                                                                                                                                                                                                          |
| ---------------------------------------------------------------------------------------- | -------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Marco Teórico sustentado en libros/papers                                                | ✅ Cumple                        | Conceptos (ZDP, Bloom, Carga Cognitiva, ITS, BKT, LLMs, multi-agente) bien citados (Vygotsky, Bloom, Sweller, Corbett, VanLehn, Vaswani, etc.).                                                                                                                                                                      |
| Estado del Arte – sección "Análisis desde la literatura" como bloque diferenciado        | ❌ No cumple                     | No existe una subsección dedicada a papers; los papers están mezclados con productos en las cuatro subsecciones temáticas                                                                                                                                                                                            |
| ≥ 7 papers descritos                                                                     | ✅ Cumple en cantidad            | Se encuentran ≈11 papers citados con descripción propia                                                                                                                                                                                                                                                              |
| Origen de papers (IEEExplore / Wiley / ScienceDirect / Springer )                        | ⚠️ No verificable desde el texto | El capítulo no indica la base/venue. Se requiere revisar las claves .bib para confirmar; varios papers parecen ser de arXiv o ACM, no de las bases solicitadas                                                                                                                                                       |
| Estado del Arte – sección "Análisis de las soluciones actuales" como bloque diferenciado | ❌ No cumple                     | No existe subsección dedicada; las soluciones están en "Tutores conversacionales" y "Herramientas para IO".                                                                                                                                                                                                          |
| ≥ 7 soluciones (productos de software)                                                   | Parcial                          | Soluciones mencionadas: Khanmigo, Socratic, Duolingo Max, ALEKS, LINGO, GAMS, CPLEX, OR-Tools, PuLP, NEOS Server, LP Assistant, OR/LP Solver, Maat, Sofía. Cantidad sobrada, pero agrupadas en un solo párrafo (LINGO/GAMS/CPLEX/OR-Tools/PuLP/NEOS comparten un mismo párrafo; LP Assistant y OR/LP Solver también) |
| Tabla comparativa con ≥ 6 criterios                                                      | ✅ Cumple                        | Tabla en líneas 162–171 con 7 criterios (LLM, Multi-agente, Específico OR, Evaluación Adaptativa, IU español, Código abierto, Detección de confusión)                                                                                                                                                                |
| Discusión post-tabla (15–20 líneas)                                                      | ❌ No cumple                     | El capítulo termina con la tabla; no hay párrafo de discusión final.                                                                                                                                                                                                                                                 |

## Hallazgos detallados

1. Estructura. La consigna pide dos subsecciones explícitas dentro de "Estado del Arte": Análisis desde la literatura y Análisis desde las soluciones actuales. El capítulo actual usa una taxonomía diferente (Tutores conversacionales / SMA educativos / Herramientas para IO / Evaluación empírica), lo que mezcla papers académicos con productos comerciales.
2. Densidad de los párrafos. Casi ningún párrafo alcanza las 8 líneas mínimas. Esto afecta especialmente a:
   - Papers: Mollick 2023, CodeHelp, Macina 2025, Moore 2022, Scaria 2024, Schmucker 2024, Kulik 2016 (todos ~2–4 líneas).
   - Soluciones: Socratic, Duolingo Max, ALEKS, Maat/Sofía (~1–3 líneas; Maat y Sofía comparten dos oraciones).
3. Agrupación indebida. Solucionadores clásicos (LINGO, GAMS, CPLEX, OR-Tools, PuLP, NEOS) están condensados en un único párrafo; deberían tener un párrafo cada uno si se quieren contar como soluciones independientes.
4. Discusión final ausente. No hay un párrafo de cierre de 15–20 líneas que explique, en base a la tabla, por qué las soluciones existentes no resuelven el problema.
5. Procedencia de las fuentes. La consigna acota las bases (IEEExplore, Wiley, ScienceDirect, Springer). Recomendable revisar el .bib para verificar y, si corresponde, complementar con papers de esas bases.
6. Errores menores observados de paso (no son parte de la consigna pero conviene corregirlos):
   - Línea 53: Developing} (llave sobrante); línea 98: xercisePracticeTool (debería ser ExercisePracticeTool); línea 31: "PI" debería ser "PE" (programación entera) para coherencia con el resto del capítulo.

## Plan de remediación propuesto

1. Reestructurar "ESTADO DEL ARTE" en dos subsecciones explícitas

```
## ESTADO DEL ARTE

### Análisis desde la literatura (papers académicos, ≥ 7 párrafos de 8–15 líneas)

### Análisis desde las soluciones actuales (productos de software, ≥ 7 párrafos de 8–15 líneas)
[tabla comparativa]
[discusión final, 15–20 líneas]
```

> Mantener el contenido valioso ya escrito, redistribuyéndolo entre las dos nuevas subsecciones.

2. Expandir cada párrafo de paper a 8–15 líneas

Mínimo 7 papers seleccionados (priorizar los más relevantes y con venue en IEEExplore/Wiley/ScienceDirect/Springer). Para cada uno incluir:

- Objetivo del trabajo y problema abordado.
- Metodología (n, diseño, dataset si aplica).
- Resultados principales con métricas.
- Limitaciones reportadas por los autores.
- Relevancia explícita para el sistema propuesto (qué decisión de diseño informa o qué brecha deja abierta).

Candidatos prioritarios: Mollick 2023, Zhang 2024 (EduAgent), Sonkar 2023 (CLASS), Macina 2023 (MathDial), Macina 2025 (MathTutorBench), Schmucker 2024 (Ruffle&Riley), Scaria 2024, Moore 2022, Kulik 2016, Ma 2014, CodeHelp.

3. Expandir cada solución a su propio párrafo de 8–15 líneas.
   Desempaquetar el bloque de solvers en párrafos individuales. Selección sugerida (≥ 7): Khanmigo, ALEKS, Duolingo Max, Socratic, LINGO, GAMS, CPLEX/OR-Tools, PuLP/NEOS Server, LP Assistant (YesChatAI), Maat (USACH), Sofía (UChile). Cada párrafo describir: propósito, tecnología subyacente, modelo de licenciamiento, alcance pedagógico, limitaciones, comparación implícita con el sistema propuesto.

4. Añadir párrafo de discusión post-tabla (15–20 líneas).
   Apoyado en las celdas de la tabla, argumentar por qué ninguna solución cubre simultáneamente: especialización en métodos de optimización + arquitectura multi-agente + evaluación adaptativa con modelo del estudiante persistente + interfaz conversacional en español + código abierto + detección de confusión. Cerrar enlazando con la propuesta de este trabajo.

5. Verificar y, si es necesario, sustituir referencias
   Auditar el .bib para confirmar que los ≥ 7 papers seleccionados provienen de IEEExplore / Wiley / ScienceDirect / Springer. Sustituir o complementar los que no califiquen. 4. Correcciones menores

## Verificación

Tras la remediación, comprobar mediante lectura corrida:

- Existencia explícita de las dos subsecciones requeridas.
- Conteo: ≥ 7 párrafos de papers, ≥ 7 párrafos de soluciones, cada uno con 8–15 líneas medidas en el render final.
- Tabla comparativa intacta con ≥ 6 criterios.
- Discusión post-tabla de 15–20 líneas presente.
- Correcciones menores aplicadas.

## Cumplimiento de chapter_02.md frente a task_02.md

### Lo que sí cumple

- Marco Teórico está bien sustentado en libros y papers (Vygotsky, Bloom, Sweller, Corbett, VanLehn, Vaswani, etc.).
- Cantidad de papers en el Estado del Arte: ~11 (sobrepasa el mínimo de 7).
- Cantidad de soluciones: ~14 mencionadas (sobrepasa 7).
- Tabla comparativa con 7 criterios (cumple el mínimo de 6).

### Lo que no cumple

1. Estructura del Estado del Arte. La tarea pide dos subsecciones explícitas: Análisis desde la literatura y Análisis desde las soluciones actuales. El capítulo usa otra taxonomía (Tutores conversacionales / SMA educativos / Herramientas IO / Evaluación empírica) que mezcla papers y productos.
2. Extensión de los párrafos. Casi ningún párrafo alcanza las 8–15 líneas requeridas. La mayoría tiene 2–4 líneas (p. ej. Moore 2022, CodeHelp, Scaria 2024, Schmucker 2024, Macina 2025, Socratic, Duolingo Max, ALEKS).
3. Soluciones agrupadas. LINGO/GAMS/CPLEX/OR-Tools/PuLP/NEOS comparten un solo párrafo; LP Assistant y OR/LP Solver también; Maat y Sofía comparten dos oraciones. Deberían ser párrafos individuales.
4. Discusión post-tabla ausente. No existe el párrafo de cierre de 15–20 líneas que la tarea exige tras la tabla comparativa.
5. Procedencia de las fuentes (IEEExplore / Wiley / ScienceDirect / Springer): no es verificable desde el texto; varios papers parecen provenir de arXiv o ACM. Conviene auditar el .bib.

> El plan de remediación detallado quedó guardado en C:\Users\Jorge Moraga Calvo\.claude\plans\based-on-the-file-zany-deer.md por si más adelante decides ejecutarlo.
