# CAPITULO 2. MARCO TEÓRICO Y ESTADO DEL ARTE

El problema que motiva este trabajo es la brecha entre la efectividad demostrada de la tutoría individual y la imposibilidad practica de ofrecerla a escala en cursos universitarios más técnicos. En la asignatura de Métodos de Optimización, los estudiantes se enfrentan a contenido matemático abstracto (programación lineal, entera y no lineal), donde la retroalimentación personalizada y oportuna puede ser determinante para el aprendizaje. Los tres objetivos específicos de este trabajo --identificar dificultades estudiantiles, desarrollar un módulo adaptativo y proveer mecanismos de retroalimentación-- requieren un fundamento tanto pedagógico como tecnológico.

Este capítulo se organiza en función de las decisiones de diseño del sistema. Primero, se presentan los fundamentos educativos que justifican los mecanismos implementados. Luego, se describe la tradición de los Sistemas de Tutoría Inteligentes (ITS) y su evolución hacia los modelos conversacionales basados en LLM. A continuación, se examinan las tecnologías de base: los modelos de lenguaje, las técnicas de prompting y los sistemas multi-agente. Para finalizar, se analiza el estado del arte, identificando las brechas que el sistema propuesto aborda.

## FUNDAMENTOS EDUCATIVOS

Las decisiones de diseño del sistema se apoyan en tres conceptos educativos que tienen un correlato directo en la implementación: la Zona de Desarrollo Próximo, la taxonomía de Bloom y la Teoría de la Carga Cognitiva.

### Zona de desarrollo próximo y andamiaje

El concepto de Zona de Desarrollo Próximo (ZDP) de \cite{Vygotsky78}, posteriormente operacionalizado como andamiaje (scaffolding) por \cite{WoodBrunerRoss}, establece que el aprendizaje ocurre cuando el estudiante recibe apoyo en el margen entre lo que puede resolver por sí mismo y lo que puede resolver con la ayuda de un guía. El tutor --humano o computacional-- debe detectar ese margen y ajustar su intervención.

En el sistema desarrollado, la (ZDP) se hace presente en tres mecanismos. Primero, la detección de la confusión por análisis de palabras clave en las respuestas del estudiante (en tres niveles: alta, media y baja) activa estrategias de explicación antes de que el estudiante pueda abandonar la tarea. En segundo lugar, la selección adaptativa entre siete estrategias pedagógicas (paso a paso, basada en ejemplos, conceptual, comparativa, geométrica, formal-matemática y analógica) ajusta la granularidad de la explicación al perfil inferido. Tercero, la evaluación en tres niveles de dificultad (básico, intermedio, avanzado) calibra los ejercicios dentro de la ZDP individual. La interfaz conversacional refuerza estos principios: el diálogo en lenguaje natural reproduce el rol de mediador que Vygotsky consideraba central para la internalización del conocimiento.

### La taxonomía de Bloom para el dominio cognitivo

La taxonomía de Bloom \citep{Bloom1956}, revisada por \cite{Anderson2001}, clasifica los objetivos de aprendizaje en seis niveles cognitivos: recordar, comprender, aplicar, analizar, evaluar y crear (ver Figura~\ref{fig:bloom}).

Esta taxonomía cumple una función normativa y operativa en el diseño del sistema desarrollado. En el plano normativo, establece que un aprendizaje profundo de los Métodos de Optimización no debe limitarse solo a que el estudiante recuerde definiciones o reproduzca procedimientos algorítmicos; requiere que sea capaz de aplicar el método símplex a un problema nuevo, analizar las condiciones de optimalidad, evaluar la pertenencia de un modelo de programación lineal frente a uno no lineal y, eventualmente, formular modelos originales para situaciones complejas.

En el plano operativo, los tres niveles de dificultad del subsistema de evaluación del presente sistema se corresponden con los estratos de la taxonomía. Los ejercicios de nivel básico evalúan las capacidades de recordar y comprender: reconocimiento de componentes de un modelo de optimización, interpretación de la función objetivo y las restricciones, e identificación de las variables de decisión. Los ejercicios de nivel intermedio apuntan a los niveles de aplicar y analizar: formulación de un problema de programación lineal a partir de un enunciado verbal, resolución del método símplex e interpretación de los resultados de dualidad. Los ejercicios de nivel avanzado corresponden a evaluar y crear: selección justificada del modelo más adecuado para un problema multivariable, diseño de un modelo de optimización para un caso de estudio, crítica de supuestos de linealidad y convexidad.

Esta correspondencia no es solo clasificatoria; orienta la generación automática de ejercicios por parte de los agentes especializados, garantizando que las evaluaciones sean apropiadas para el nivel de cada estudiante y que el sistema pueda rastrear el progreso a lo largo de la jerarquía cognitiva.

### Teoría de la carga cognitiva

La Teoría de la Carga Cognitiva de \cite{Sweller1988} distingue entre carga intrínseca (inherente a la complejidad del material), carga extrínseca (impuesta por un diseño instruccional deficiente) y carga germana (esfuerzo cognitivo invertido en construir esquemas; ver Figura~\ref{fig:cognitiveload}). La implicación para el diseño instruccional es reducir la carga extrínseca y gestionar la intrínseca para maximizar la germana.

Se eligió la arquitectura multi-agente como estrategia de gestión de la carga intrínseca: cada agente se especializa en un subdominio (IO general, modelado matemático, PL, PI, PNL), evitando que el estudiante navegue simultáneamente por la totalidad del espacio de conocimiento. Además, el patrón de selección directa --el estudiante elige con qué agente interactuar-- no solo es una decisión de interfaz: exige clasificar la consulta dentro del mapa de subdominios, lo que constituye un ejercicio metacognitivo que genera carga germana \citep{Sweller1988}. Por último, la interfaz conversacional en lenguaje natural elimina la carga extrínseca asociada a sistemas de menús o formularios.

### Sistemas de tutoría inteligente

Los sistemas de tutoría inteligente (ITS) constituyen la tradición tecnológica dentro de la cual se inscribe el presente trabajo. Desde su emergencia en la década de los 70 del siglo pasado, los ITS han buscado replicar, mediante software, la efectividad pedagógica del tutor humano uno a uno. Esta sección examina la arquitectura clásica de los ITS, el problema pedagógico que motivó su desarrollo y la evolución de estos sistemas hacia los tutores conversacionales basados en modelos de lenguaje de gran escala (LLM).

#### El problema de los dos sigma y la motivación de los ITS

La motivación fundacional de los ITS proviene del trabajo de \cite{Bloom1984}, quien documentó que el estudiante promedio bajo tutoría individual uno a uno se ubicaba dos desviaciones estándar por encima del estudiante promedio de instrucción convencional en aula. Esto equivale a que un estudiante del percentil $50$ con tutor individual superaría al $98\%$ de los estudiantes en aula. Bloom denominó este hallazgo ``el problema de los dos sigma'' porque, si bien la superioridad era evidente, proveer tutoría individual a escala resultaba inviable. La pregunta que motivó décadas de investigación en ITS fue: ¿puede un sistema computacional emular los mecanismos clave de la tutoría individual y ofrecerlos a escala?

#### Arquitectura clásica de los sistemas de tutoría inteligente

La arquitectura canónica de los ITS, consolidada por \cite{Sleeman1982}, \cite{Wenger1987} y \cite{Corbett1994}, descompone el sistema en cuatro módulos (ver Figura~\ref{fig:itsarch}): el modelo de dominio (conocimiento que se enseña), el modelo del estudiante (representación dinámica de lo que el aprendiz sabe), el \textbf{modelo pedagógico} (estrategias instruccionales) y la \textbf{interfaz de usuario}.

En el sistema desarrollado, estos cuatro módulos se implementan de la siguiente forma. El modelo de dominio se distribuye entre cinco agentes especializados, cada uno con prompts de sistema que codifican el conocimiento de su subdominio. El modelo del estudiante se mantiene en PostgreSQL: niveles de conocimiento por tema (campos JSON en la tabla Student), maestría por concepto (StudentCompetency, calculada mediante promedio exponencialmente ponderado con $\alpha = 0.3$) e historial de evaluaciones y sesiones de repaso. El modelo pedagógico se implementa en la detección de confusión (utils.py), la selección de estrategias de explicación y la generación adaptativa de ejercicios con progresión por rangos. La interfaz es una aplicación conversacional en Streamlit.

#### Modelamiento del estudiante

\label{sec:student_model}
El modelo referencial en la literatura es Bayesian Knowledge Tracing (BKT) de \cite{Corbett1994}, un modelo oculto de Markov que estima probabilísticamente si el estudiante domina cada componente de conocimiento. El sistema desarrollado no implementa BKT; en su lugar, se optó por un modelo determinístico basado en promedio exponencialmente ponderado (EWA), que resultó más adecuado para el contexto de uso:

- Cada concepto del dominio tiene un puntaje de maestría entre $0.0$ y $1.0$, actualizado tras cada evaluación: $score = \alpha \cdot score_{nuevo} + (1 - \alpha) \cdot score_{anterior}$, con $\alpha = 0.3$.
- Se definen cinco niveles de maestría con umbrales y requisitos mínimos de intentos: Not Started (0 intentos), Novice ($< 0.30$), Developing ($\geq 0.30$), Proficient ($\geq 0.60$ y $\geq 3$ intentos) y Mastered ($\geq 0.85$ y $\geq 5$ intentos).

Este modelo se complementa con un sistema de repetición espaciada \citep{Ericsson2016} (SM-2) para la retención a largo plazo. El algoritmo SM-2 programa revisiones con intervalos crecientes $[1, 3, 7, 14, 30, 60]$ días, ajustados por un factor de facilidad que se modifica según la calidad de cada respuesta (escala $0-5$). Si la calidad es inferior a $3$, el intervalo se reinicia a $1$ día.

#### Retroalimentación formativa

La efectividad de los ITS está fuertemente asociada con la provisión de retroalimentación inmediata y específica \citep{VanLehn2011}. El meta-análisis de \cite{VanLehn2011} encontró que los ITS producen mejoras de $0.76$ a $1.0$ desviaciones estándar sobre la instrucción convencional, y que el factor determinante es la retroalimentación paso a paso (step-level feedback), no la retroalimentación a nivel de tarea completa.

El sistema implementa retroalimentación formativa en dos niveles. A nivel de evaluación, el servicio de calificación (GradingService) genera retroalimentación detallada para cada respuesta, especificando qué aspectos del razonamiento son correctos, cuáles son incorrectos y por qué, con referencia a los conceptos teóricos relevantes y una calificación en escala $1.0$--$7.0$ basada en rúbricas. A nivel conversacional, los agentes identifican errores conceptuales implícitos en las preguntas del estudiante y los abordan antes de proporcionar la explicación, siguiendo el principio socrático de no entregar soluciones directas.

#### Limitaciones de los ITS clásicos

Los ITS clásicos presentan tres limitaciones que motivaron la transición hacia sistemas basados en LLM. Primera, la dependencia de la ingeniería del conocimiento: construir un modelo de dominio completo requiere años de trabajo de equipos interdisciplinarios y no escala a dominios amplios \citep{Koedinger2006}. Segunda, la rigidez de la interfaz: formularios y entornos estructurados no permiten interacción en lenguaje natural libre. Tercera, la incapacidad de manejar la ambigüedad del lenguaje estudiantil: los errores de comprensión se expresan frecuentemente en razonamientos parciales y formulaciones imprecisas que los ITS clásicos no pueden interpretar.

Los LLM resuelven estas tres limitaciones: su conocimiento paramétrico elimina la ingeniería de dominio manual, su capacidad generativa habilita interfaces conversacionales y su procesamiento del lenguaje natural permite interpretar consultas ambiguas. El sistema desarrollado integra estas capacidades con la estructura pedagógica de los ITS clásicos: agentes especializados por dominio, modelo del estudiante persistente y evaluación adaptativa.

### Tecnologías de base

#### Modelos de lenguaje de gran escala (LLM)

Los LLM que el sistema soporta, GPT (OpenAI), Claude (Anthropic) y Gemini (Google DeepMind), son transformers decoder-only \citep{Vaswani2017} preentrenados sobre corpus de billones de tokens. El preentrenamiento a escala produce capacidades emergentes: razonamiento multi-paso, resolución de problemas matemáticos y comprensión de instrucciones complejas \citep{Wei2022}. El ajuste mediante instrucciones y el aprendizaje por refuerzo con retroalimentación humana (RLHF) \citep{Ouyang2022} los transformó en asistentes capaces de seguir instrucciones, lo que resulta fundamental para su uso como motor de agentes tutores.

El sistema abstrae las diferencias entre proveedores mediante un servicio (LLMService) que implementa el patrón Adapter: una interfaz común permite intercambiar proveedores sin modificar la lógica de los agentes. Esta decisión responde a criterios de resiliencia (no depender de un único proveedor) y de costo (permitir seleccionar el modelo según la relación calidad/precio para cada tarea).

#### Ingeniería de prompts

\label{sec:prompting}
El prompt del sistema de cada agente encapsula su identidad pedagógica: rol, subdominio, estrategias de explicación, criterios de detección de confusión y restricciones temáticas. Los prompts se construyen dinámicamente mediante el método build_enhanced_system_prompt(), que incorpora el nivel de confusión detectado, los recordatorios de repetición espaciada y el contexto del estudiante.

Se emplean tres técnicas de prompting:

- Role prompting: establece la especialización del agente. El agente de Programación Lineal responde únicamente dentro de su ámbito y deriva consultas fuera de él al agente de IO general.
- Chain-of-thought prompting \citep{Wei2022b}: guía al modelo para descomponer su razonamiento en pasos explícitos, lo cual es valioso para explicar procedimientos como el método Símplex.
- Few-shot prompting \citep{Brown2020}: incluye ejemplos de interacciones correctas calibrados al nivel del estudiante (principiante, intermedio, avanzado).

La gestión del historial de conversaciones es un aspecto crítico: los LLM no tienen memoria persistente entre llamadas. El sistema mantiene el historial en PostgreSQL e inyecta los últimos 10 mensajes relevantes en el contexto de cada llamada a la API, lo que permite coherencia a lo largo de sesiones extendidas. Se implementan así dos niveles de memoria: a corto plazo (contexto activo de la conversación) y a largo plazo (niveles de conocimiento, competencias y sesiones de repaso almacenados en la base de datos).

#### Sistemas multi-agente basados en LLM

Los sistemas multi-agente (SMA) son sistemas compuestos por múltiples entidades autónomas que perciben su entorno, razonan y actúan para alcanzar objetivos \citep{Wooldridge1995}. La motivación para adoptar este paradigma en lugar de un agente monolítico es que los LLM degradan su rendimiento cuando deben mantener simultáneamente múltiples marcos de conocimiento especializado en el contexto activo \citep{Qian2023}. La especialización por subdominio permite que cada agente mantenga un contexto focalizado.

Se eligió un patrón de selección directa, es decir, el estudiante selecciona explícitamente el agente con el que interactúa a través de la interfaz, sin un agente orquestador automático. Esta decisión se fundamenta pedagógicamente porque exige que el estudiante clasifique su consulta dentro del mapa de subdominios antes de formularla, lo que constituye un ejercicio metacognitivo alineado con la carga germana de \cite{Sweller1988}.

Los agentes del sistema extienden sus capacidades mediante el patrón de uso de herramientas (tool use), documentado por \cite{Xi2023} y \cite{Wang2025}. Cada agente puede invocar herramientas especializadas implementadas como extensiones de BaseTool de LangChain:

- Herramientas de modelado: validación de modelos matemáticos (ModelValidatorTool), resolución de problemas (ProblemSolverTool), visualización de regiones factibles (RegionVisualizerTool), práctica de ejercicios (ExercisePracticeTool) y validación de formulaciones estudiantiles (ExerciseValidatorTool).
- Herramientas de IO: clasificación de problemas de optimización (ProblemClassifierTool) y exploración de contexto histórico (TimelineExplorerTool).
- Herramienta de repaso: gestión de sesiones de repetición espaciada (SpacedRepetitionReviewTool).

El servicio \texttt{LLMService} coordina el ciclo de ejecución de herramientas: el LLM genera llamadas a herramientas, el servicio las ejecuta y devuelve los resultados al modelo para que genere la respuesta final, con un máximo de 3 iteraciones por turno.

LangChain \citep{Chase2026} es el framework de orquestación utilizado para coordinar las interacciones entre los LLM, las herramientas y el historial de conversación. Se eligió sobre alternativas como AutoGen \citep{Wu2023} y LlamaIndex por su madurez, amplitud de integraciones con proveedores LLM y compatibilidad con el stack del proyecto (FastAPI, PostgreSQL).

## ESTADO DEL ARTE

La revisión del estado del arte se organiza en torno a los criterios que definen las brechas que el sistema propuesto aborda: (1) si el sistema utiliza LLM, (2) si implementa una arquitectura multi-agente, (3) si está especializado en el dominio de Métodos de Optimización, (4) si mantiene un modelo del estudiante persistente con evaluación adaptativa, (5) si ofrece una interfaz conversacional en español y (6) si es de código abierto.

### Tutores conversacionales basados en LLM

Khanmigo (Khan Academy + OpenAI, \citep{Khanacademy}) es el caso más prominente de integración de LLM en educación a escala. Opera como tutor socrático sobre GPT-4 y cubre un amplio espectro de materias. Su enfoque socrático ---formular preguntas en lugar de dar respuestas directas--- informó el diseño de los prompts del sistema desarrollado, que incluyen restricciones contra la entrega de soluciones. Sin embargo, Khanmigo es un agente único generalista: no segmenta el dominio en subdominios especializados, no cubre Investigación Operativa y su disponibilidad en español es parcial.

Socratic (Google, \citep{SocraticWiki}) fue una aplicación que permitía a los estudiantes fotografiar problemas y recibir explicaciones; se fusionó con Google Lens en 2025. Su enfoque es puramente reactivo: no mantiene un modelo del estudiante ni adapta su comportamiento entre sesiones.

Duolingo Max \citep{Duolingo2023} incorpora funcionalidades basadas en GPT-4 para la explicación de errores y la práctica conversacional en idiomas. Si bien es cierto que el dominio no es el mismo, es relevante como referencia de integración LLM en plataformas educativas masivas. Su arquitectura es de agente único con modelado implícito del estudiante.

El trabajo de \cite{Mollick2023} sistematizó el uso de GPT-4 como tutor universitario mediante prompts cuidadosamente diseñados, demostrando que los LLM de propósito general pueden actuar como tutores con la ingeniería de prompts adecuada, pero sin ofrecer una arquitectura replicable ni persistencia del estado del estudiante.

La limitación transversal de estos sistemas es su naturaleza generalista: ninguno está especializado en Métodos de Optimización ni implementa una arquitectura multi-agente que segmente la complejidad del dominio.

### Sistemas multi-agente educativos

EduAgent \citep{Zhang2024} coordina agentes especializados para generar planes de estudio personalizados, demostrando que la descomposición en agentes mejora la coherencia pedagógica respecto a un agente único. La lección para el sistema desarrollado fue la validación del principio de especialización. Sin embargo, EduAgent opera en modo batch (genera materiales estáticos) y no implementa una interfaz conversacional en tiempo real.

\cite{Sonkar2023} proponen CLASS, un marco de desarrollo de ITS con LLM que establece la separación de roles entre el agente pedagógico y el agente de evaluación para preservar la integridad del proceso. Este principio se adoptó en el sistema desarrollado: los agentes tutores y el servicio de evaluación (GradingService) están desacoplados.

\cite{Macina2023} documentaron en MathDial ($2.900$ conversaciones de tutoría en matemáticas) que los LLM tienen tendencia a resolver los problemas directamente para el estudiante en lugar de guiarlo. Este hecho influyó en el diseño de los prompts del sistema, que incluyen restricciones explícitas contra la entrega directa de soluciones favoreciendo el método socrático.

El trabajo de \cite{10.1145/3631802.3631830} sobre CodeHelp introduce la separación entre un agente de análisis y un agente de retroalimentación pedagógica para evitar la generación de soluciones directas. El sistema desarrollado aplica un principio análogo en la separación agente-tutor y el servicio de evaluación.

\cite{Macina2025} proponen MathTutorBench, un benchmark que demuestra que la experticia en matemáticas no se traduce automáticamente en efectividad pedagógica: los modelos más potentes tienden a resolver problemas directamente. Esta evidencia reforzó la decisión de implementar restricciones de rol socrático en los prompts.

### Herramientas para Investigación Operativa

Las herramientas existentes para Métodos de Optimización son, en su mayoría, solucionadores: LINGO, GAMS, CPLEX, OR-Tools \citep{GoogleOR}, PuLP \citep{Mitchell2011} y NEOS Server \citep{Czyzyk1998}. Reciben un modelo matemático y devuelven una solución óptima, pero no explican conceptos, no detectan errores de comprensión, no adaptan la dificultad y no conversan con el estudiante.

ALEKS \citep{Aleks}, fundamentado en la Teoría de Espacios de Conocimiento \citep{Falmagne2015}, es la plataforma adaptativa de mayor implantación en matemáticas universitarias. Diagnostica el estado de conocimiento mediante evaluaciones breves y genera trayectorias individualizadas, con evidencia documentada de mejoras en tasas de aprobación \citep{McGraw-Hill2018}. Sin embargo, no cubre Investigación Operativa, no dispone de interfaz conversacional y opera con ejercicios de respuesta cerrada.

Han emergido asistentes conversacionales para PL basados en GPT-4o, como Linear Programming Assistant y Operations Research / Linear Programming Solver \citep{YesChatAI2024a, YesChatAI2024b}. Demuestran que un LLM con prompts adecuados puede responder consultas técnicas con corrección aceptable. Sin embargo, no mantienen un modelo del estudiante (cada sesión es independiente), no implementan evaluación adaptativa, no ofrecen retroalimentación formativa estructurada, no están disponibles en español y son servicios comerciales sin código abierto.

En el contexto local, el Departamento de Ingeniería Industrial de la Universidad de Santiago de Chile presentó, en el segundo semestre de 2024, la asistente virtual Maat, destinada a potenciar la experiencia educativa, lo que evidencia un interés institucional en la adopción de estas tecnologías \citep{Darvishi2024}. Por su parte, la Universidad de Chile cuenta con Sofía.

### Evaluación empírica de ITS basados en LLM

\cite{Moore2022} demostraron que GPT-3 puede clasificar preguntas según calidad pedagógica con niveles de concordancia comparables a evaluadores humanos, evidencia temprana de la viabilidad de LLM como evaluadores automáticos. \cite{Scaria2024} encontraron que el $78\%$ de las preguntas generadas por GPT-4 alineadas con Bloom eran de alta calidad, y que las instrucciones chain-of-thought con ejemplos producen mejores resultados que los prompts excesivamente detallados. Este hallazgo orientó el diseño de los prompts de generación de evaluaciones del sistema.

\cite{Schmucker2024} evaluaron Ruffle\&Riley ($N = 200$) y encontraron un alto engagement pero sin diferencias significativas en las ganancias de aprendizaje a corto plazo medidas por pre/post-test, resultado consistente con \cite{VanLehn2011}: los efectos de la tutoría conversacional se manifiestan en comprensión profunda y transferencia, no en recuerdo inmediato.

El meta-análisis de \cite{Ma2014} ($107$ estudios, $14.321$ participantes) encontró que los ITS producen ganancias significativas sobre la instrucción convencional ($g = 0.42$) y la instrucción computacional no inteligente ($g = 0.57$), sin diferencias significativas respecto a la tutoría humana individual ($g = -0.11$). \cite{Kulik2016} reportó un efecto mediano de $g = 0.66$ en 50 estudios controlados. Estos resultados corroboran la viabilidad del enfoque ITS.

Para la validación del sistema desarrollado, se planifica un diseño cuasi experimental de pre/post-test con estudiantes de la asignatura, combinado con una encuesta de usabilidad (SUS, \citep{Brooke1996SUS}) y análisis de registros de interacción.

### Tabla comparativa y brechas identificadas

La Tabla~\ref{table:compare} sintetiza las características de los sistemas revisados. Los criterios de comparación corresponden a las funcionalidades que la literatura identifica como determinantes para la efectividad de un ITS en dominios técnicos: uso de LLM (capacidad conversacional), arquitectura multi-agente (especialización de dominio), especificidad en OR (cobertura del dominio objetivo), evaluación adaptativa (ajuste al nivel del estudiante), interfaz en español (accesibilidad para la población objetivo), código abierto (replicabilidad) y detección de confusión (adaptación en tiempo real).

✅
:white_check_mark:
:x:

| Sistema           | Basado en LLM      | Multi-agente       | Específico OR      | Evaluación Adaptativa | IU español         | Código abierto     | Detección confusión |
| ----------------- | ------------------ | ------------------ | ------------------ | --------------------- | ------------------ | ------------------ | ------------------- |
| Khanmigo (2023)   | :white_check_mark: | :x:                | :x:                | Parcial               | Parcial            | :x:                | :x:                 |
| Socratic          | :white_check_mark: | :x:                | :x:                | :x:                   | :x:                | :x:                | :x:                 |
| Duolingo          | :white_check_mark: | :x:                | :x:                | :x:                   | Parcial            | :x:                | :x:                 |
| ALEKS             | :x:                | :x:                | :x:                | :white_check_mark:    | Parcial            | :x:                | :x:                 |
| EduAgent          | :white_check_mark: | :white_check_mark: | :x:                | Parcial               | :x:                | Parcial            | Parcial             |
| LINGO / GAMS      | :x:                | :x:                | :white_check_mark: | :x:                   | :x:                | Parcial            | :x:                 |
| LP Assistant      | :white_check_mark: | :x:                | :white_check_mark: | :x:                   | :x:                | :x:                | :x:                 |
| Sistema propuesto | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark:    | :white_check_mark: | :white_check_mark: | :white_check_mark:  |
