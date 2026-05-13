# Desarrollo de agente virtual basado en inteligencia artificial para apoyo a estudiantes de métodos de optimización en las carreras de Ingeniería Civil en Informática e Ingeniería de Ejecución en Computación e Informática

## INTRODUCCIÓN

### ANTECEDENTES Y MOTIVACIÓN

La educación, ya sea primaria, secundaria o superior, no ha estado ajena a los impactos que ha generado el auge, en los últimos años, de las herramientas impulsadas por la IA generativa, representadas en los grandes modelos de lenguaje (LLM, por sus siglas en inglés) \citep{Yigci2024}. Esto ha provocado tanto inquietudes como entusiasmo, ya sea por desconfianza hacia las soluciones tecnológicas o por la necesidad de desarrollar competencias digitales \citep{Miao2024}.

En este contexto, las primeras preocupaciones sobre el uso de las nuevas tecnologías se han centrado en si es mejor prohibir su uso o adoptar un enfoque progresivo en los entornos educativos \citep{Miao2024, Yigci2024}. En las universidades que han adoptado el uso de IA (como en algunas de EE.UU. y la incorporación de ChatGPT Edu, han surgido voces de alerta y críticas \citep{Purser2025}. Entre estas, se sostiene que estas tecnologías convierten el conocimiento en datos y que capacidades humanas valiosas —como la curiosidad y el discernimiento—, podrían desaparecer \citep{Purser2025}; por lo que el resultado no es inteligencia aumentada, sino aprendizaje simulado. Otra crítica se relaciona con que los profesores ya no estarían enseñando a pensar mejor, sino a cómo redactar mejores \textit{prompts} \citep{Purser2025}. Y que el trabajo final de la universidad, la tesis, es solo un ritual vacío en el que los estudiantes tienen que cumplir: pagar por tener el privilegio de participar en el teatro del aprendizaje falso \citep{Purser2025}.

Aun así, ya sea para bien o para mal, estas herramientas están transformando la manera en que se generan y se ofrecen contenidos de enseñanza y aprendizaje \citep{Miao2024}, y lo que ``impone'' la IA es que ha llegado para quedarse \citep{Sigman2023}. La cita que abre este capitulo puede ser vista tanto como una advertencia como una resistencia al cambio —en este caso, la transición de la oralidad a la escritura en tiempos de Sócrates—. Frente a ciertos cambios, somos cautelosos, como innovar en la estructura de un puente; frente a otros, nos sumamos imprudentemente a la ola del cambio, adoptando cada moda que emerge sin pensar en los riesgos \citep{Sigman2023}. Esto es especialmente crítico en la educación, considerando que es la herramienta más importante de la que disponen las sociedades para modelar su futuro \citep{Sigman2023}. Pero, por otro lado, permanecer inmóvil puede ser perjudicial, lo que nos lleva a preguntar: ¿qué transformaciones debería experimentar la educación y qué principios no deberían cambiar? \citep{Sigman2023}. Según \cite{Sigman2023}, los pilares básicos de la cognición intrínseca a la educación que deberían mantenerse son: la capacidad de concentrarnos, la competencia lectora, el buen uso del lenguaje y el pensamiento lógico-matemático, entre otros.

Por su parte, el aprendizaje es una actividad de alto costo energético para los organismos, y en el caso del aprendizaje humano, este costo se incrementa debido a su naturaleza cultural, lo que implica un elevado costo social y económico \citep{Pozo2008}. Es decir, aprender no es gratis; requiere un esfuerzo individual significativo y la asignación de recursos sociales, tecnológicos y económicos para distribuir el conocimiento a nivel social \citep{Pozo2008}.

Por otro lado, uno de los aspectos llamativos del fracaso en entornos educativos no es solo el número de estudiantes que pueden llegar a reprobar, sino aquellos/as que aprueban sin haber adquirido un aprendizaje significativo \citep{Pozo2008}. A ello se suma que un aprendizaje incorrecto lleva más tiempo, ya que des-aprender conceptos erróneos puede resultar más complicado que aprenderlos correctamente desde un comienzo \citep{Ortiz2009}. Además, la falta de apoyo personalizado puede ser desmotivadora, especialmente cuando no se ofrecen escenarios de aprendizaje diversos que fomenten la atención y la motivación estudiantil \citep{Pozo2008}. Esta situación se ve reforzada por la limitada disponibilidad de tiempo de los docentes, lo que reduce la retroalimentación individual y, por otro lado, el aprendizaje es el resultado de la práctica \citep{Pozo2008}, especialmente si esta es enfocado \citep{Ericsson2016}. No obstante, lograr una práctica constante y personalizada en un entorno de clase tradicional puede ser complicado \citep{Pozo2008}, lo cual es esencial para resolver problemas de alta conceptualización matemática como los que se presentan en optimización.

Este escenario abre la oportunidad de explorar de qué manera las herramientas impulsadas por IA generativa pueden integrarse en asignaturas específicas para potenciar el aprendizaje y la resolución de problemas complejos, considerando que estas tecnologías tienen el potencial de hacer que la educación sea más accesible, asequible y efectiva \citep{Crompton2023, Yigci2024}. Entre sus posibles usos se incluyen personalizar el aprendizaje, brindar apoyo estudiantil y automatizar tareas administrativas, además de la creación de nuevas oportunidades educativas \citep{Crompton2023, Junaid2024, Yigci2024}.

La evidencia empírica muestra que esta tecnología tiene un impacto significativo en los resultados generales del aprendizaje, influyendo en los logros académicos, el razonamiento explícito y la retención de conocimientos \citep{Labadze2023}. Este efecto positivo es especialmente relevante cuando se considera el potencial de las herramientas de IA para mejorar tanto el éxito como la participación estudiantil, particularmente de aquellos provenientes de contextos desfavorecidos
\citep{Labadze2023}.

Para el cuerpo estudiantil, los asistentes virtuales impulsados por IA ofrecen múltiples ventajas, como la asistencia en tareas y estudios \citep{Labadze2023}. Pueden proporcionar comentarios detallados sobre las tareas, identificando áreas de mejora y sugiriendo estrategias para un aprendizaje más profundo \citep{Celik2022}. Asimismo, pueden ofrecer soluciones paso a paso y guiar en la resolución de problemas complejos, lo que permite la autoevaluación, el refuerzo de conocimientos y la preparación para pruebas y exámenes \citep{Labadze2023}.

Simultáneamente, para el cuerpo docente, los asistentes virtuales representan una herramienta valiosa para optimizar el tiempo \citep{Junaid2024, Labadze2023}, ya que pueden asumir tareas rutinarias como la calificación, proporcionar información y generar diversos tipos de preguntas y respuestas en diferentes disciplinas \citep{Labadze2023}. La utilización de asistentes virtuales también tiene el potencial de enriquecer la pedagogía, permitiendo a los/las educadores/as mejorar su enseñanza y ofrecer apoyo especializado que se ajuste a las necesidades, intereses y preferencias de aprendizaje de cada estudiante \citep{Labadze2023}.

En síntesis, la integración de asistentes virtuales impulsados por IA en los entornos educativos promete transformar la manera en que los/las estudiantes aprenden e interactúan con la información \citep{Labadze2023}.

### PLANTEAMIENTO DEL PROBLEMA

### SOLUCIÓN PROPUESTA

El curso de Métodos de Optimización presenta desafíos importantes a los/las estudiantes para adquirir una comprensión de los conceptos y técnicas involucradas. Esta situación se ve amplificada por la falta de recursos educativos que se adapten a los diferentes estilos y ritmos de aprendizaje de cada estudiante. Además, la falta de apoyo y retroalimentación más personalizada contribuyen a una experiencia de aprendizaje que puede no satisfacer las necesidades individuales. Por lo tanto, es importante identificar cómo es posible mejorar la experiencia educativa en este curso en particular, abordando la necesidad de un enfoque más adaptativo y centrado en el alumno/a que permita un aprendizaje más efectivo.

#### Características de la solución

La solución propuesta consiste en una plataforma educativa que aborda parte del programa del curso de Métodos de Optimización, diseñada para apoyar la enseñanza y el aprendizaje. Sus principales características incluyen inteligencia artificial, mecanismos de aprendizaje adaptativo y sistemas de gestión de la información, entre otras características. A continuación, se describen sus principales componentes funcionales.

##### Arquitectura de tutoría multi-agente

Una de las características de la plataforma es la integración de cinco agentes de IA especializados, cada uno responsable de un tema que se aborda en el programa del curso: Investigación de Operaciones, Programación Lineal, Modelado Matemático, Programación Entera y Programación No Lineal. Estos agentes operan mediante un registro multi-agente que asigna el agente adecuado a las interacciones de los estudiantes según el tema seleccionado. Cada agente cuenta con indicaciones específicas del dominio, bases de conocimiento seleccionadas (no todos) y mecanismos adaptativos compartidos, como la detección de confusiones y la selección de estrategias.

##### Interfaz de aprendizaje conversacional

El sistema ofrece un entorno de aprendizaje interactivo basado en chat donde los estudiantes pueden participar en diálogos con el tutor de IA. La interfaz mantiene un historial de las conversaciones (10), permite la selección dinámica de temas y proporciona retroalimentación en tiempo real.

##### Aprendizaje adaptativo y personalización

El aprendizaje adaptativo se implementa a través de la detección de confusiones (detección de palabras clave), el análisis de las respuestas de los estudiantes y el modelado de las preferencias de aprendizaje. La plataforma puede modificar sus estrategias de explicación, ofrecer vías de enseñanza alternativas y actualizar el nivel de conocimientos del estudiante en función de su rendimiento en evaluaciones (mediante promedio exponencialmente ponderado en StudentCompetency); sin embargo, la actualización automática del nivel durante la conversación aún no está implementada.

##### Sistema de evaluación y calificación

La plataforma incorpora la generación y calificación automatizada de evaluaciones, impulsada por LLM. Genera preguntas personalizadas, además de contar con una base de ejercicios (actualmente, el modelado matemático es el más completo en este aspecto) con diferentes niveles de dificultad y emplea rúbricas estructuradas en una escala de calificación de 1.0 a 7.0. Admite calificación automatizada y se genera retroalimentación detallada para cada entrega. La calificación manual por parte del docente es una funcionalidad fuera del alcance de la implementación actual.

##### Seguimiento y análisis del progreso

El sistema rastrea indicadores de rendimiento, incluyendo niveles de conocimiento específicos de cada tema, cronogramas de actividades, historial de evaluaciones y datos conversacionales. Esto permite un análisis del progreso del aprendizaje y proporciona al estudiante información sobre su desarrollo.

##### Gestión de usuarios, autenticación y herramientas de administración

La solución implementa autenticación mediante tokens JWT, hash de contraseñas y control de acceso basado en roles. Las funciones administrativas incluyen la gestión de usuarios, la supervisión del sistema, la configuración de proveedores LLM y la visualización de métricas.

##### Arquitectura de frontend y backend

El frontend, desarrollado con Streamlit, ofrece una navegación estructurada mediante chat, evaluación, visualización del progreso y paneles de administración. El backend, con FastAPI, emplea una arquitectura orientada a servicios que facilita la modularidad, la escalabilidad y la integración con múltiples proveedores de LLM. Un esquema de base de datos relacional almacena usuarios, conversaciones, mensajes, evaluaciones y retroalimentación.

#### Propósito de la solución

El objetivo general de la solución propuesta es proporcionar una plataforma tecnológica y pedagógica que mejore la experiencia de aprendizaje en Métodos de Optimización. Más específicamente, la solución busca:

##### Facilitar una educación accesible y personalizada

Al combinar la tutoría de IA multi-agente con el aprendizaje adaptativo, el sistema ofrece instrucción personalizada. Esto responde directamente a la necesidad de retroalimentación individualizada en asignaturas técnicas, donde la comprensión conceptual puede variar significativamente entre los alumnos.

##### Apoyo a la enseñanza de conceptos complejos

El sistema está diseñado para facilitar la comprensión del alumnado de contenido matemático intensivo. Mediante agentes de IA especializados, ofrece explicaciones adaptadas a temas básicos, intermedios y avanzados, abarcando tanto la dimensión teórica como la práctica.

##### Creación de ejercicios y evaluaciones

Otro objetivo es la automatización de los procesos de evaluación. La plataforma genera ejercicios, rúbricas de calificación y \textit{feedback}, lo que permitiría a los profesores reducir el tiempo dedicado a estas tareas y centrarse en decisiones pedagógicas de mayor nivel.

##### Monitoreo del progreso estudiantil

Los estudiantes obtienen información sobre su aprendizaje, mientras que los profesores pueden analizar los patrones de participación y rendimiento del sistema.

# Críticas

1. Sección Solución propuesta es muy débil.
   - Afirmaciones sin ningún sustento desde la literatura.
2. Buscar papers (de 10 a 15) para dar mayor sustento al trabajo (dentro de los últimos 5 años) donde se pueda encontrar información respecto de las dificultades importantes que existen en la enseñanza/aprendizaje de los cuatro temas elegidos:
   - Modelado Matemático.
   - Programación Lineal.
   - Programación Entera.
   - Programación No Lineal.

## Papers encontrados

- Kenney, R., An, T., Kim, S. H., Uhan, N. A., Yi, J. S., & Shamsul, A. (2020). Linear programming models: identifying common errors in engineering students’ work with complex word problems. International Journal of Science and Mathematics Education
- Peddapalli, N., & Sadhukhan, S. (2024, December). Analysis of Problem-Based Learning on Undergraduate Students’ Problem-Solving Skills in Operation Research Course–A Case Study. In International Conference on Technology
- Cambazard, H., Catusse, N., Brauner, N., & Lemaire, P. (2022). Teaching OR: automatic evaluation for linear programming modelling.
- Rellon, L. R. S., & Corsonado, J. C. (2024). Students’ procedural knowledge on simplex method in linear programming: An explanatory sequential design.
- Octaria, D., Zulkardi, Z., & Putri, R. I. I. (2023). Systematic Literature Review: How students learn linear programming with realistic mathematics education?
- Rocha, H., & Babo, A. (2024). Problem-solving and mathematical competence: A look to the relation during the study of Linear Programming
