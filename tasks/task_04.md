# Task four

## Arquitectura de la aplicación

### Vista Lógica

La Vista Lógica organiza el sistema en módulos o componentes que representan las principales funcionalidades, como autenticación, procesamiento de pagos o gestión de usuarios, y muestra cómo estos se relacionan e interactúan entre sí para cumplir con los requisitos funcionales del sistema. Esta vista facilita la comprensión de la estructura funcional y las responsabilidades de cada componente, permitiendo una visión clara de "qué hace" cada parte del sistema.

### Vista de Despliegue

Describe la infraestructura física en la que el sistema se ejecuta, incluyendo servidores, redes y otros recursos necesarios para soportar la aplicación. En esta vista se asignan los distintos componentes de software a la infraestructura, asegurando que el sistema cumpla con requisitos no funcionales como disponibilidad, escalabilidad y rendimiento.

### Vista de Implementación

Detalla la organización del código fuente y la estructura de los archivos, paquetes y dependencias en el repositorio de código, lo que permite a los desarrolladores entender cómo está estructurado el software para facilitar su desarrollo y mantenimiento.

### Vista de Datos

La Vista de Datos describe las tablas de la Base de Datos y sus respectivas relaciones entre ellas.

#### Task

En todas las vistas se requiere **incluir una imagen que describa de manera gráfica la vista**. Luego, después de la imagen se debe proceder a **describir en detalle la vista haciendo referencia a la imagen**.

## Application Architecture

### Logical View

The Logical View organizes the system into modules or components that represent the main functionalities, such as authentication, payment processing, or user management, and shows how these relate and interact with each other to meet the system's functional requirements. This view facilitates understanding the functional structure and responsibilities of each component, allowing a clear view of **what** each part of the system does.

Logical view summary:

- Shows the key abstractions in the system as objects or classes of objects.
- It should be possible to relate the system requirements to the entities.
- Class diagrams or communication diagrams are used.

#### Main architectural problems in currently diagram

1. The API layer is mixing responsibilities

Currently:

```
Auth --> Routes --> Registry --> Agents
```

This suggests:

- authentication
- routing
- orchestration
- dependency resolution

Are all happening inside the API layer. That becomes messy over time. A better separation maybe:

```
FastAPI Routes
↓
Application/Orchestration Layer
↓
Agents / Services
```

Meaning:

- routes only validate HTTP requests/responses
- orchestration coordinates workflows
- agents solve tasks

Right now your agents are acting partly like application services.

---

#### Recommended fix / update

Add an orchestration/application layer.

Example:

```mermaid
subgraph App["Application Layer"]
    Tutor["tutoring_orchestrator"]
    Workflow["workflow_manager"]
end
```

Then:

```
Routes --> App --> Registry --> Agents
```

This is MUCH cleaner.

2. Agents directly using tools AND services can become chaotic

You currently have:

```
Agents --> Services
Agents --> Tools
```

This is acceptable for MVPs, but eventually creates:

- duplicated logic
- hidden dependencies
- inconsistent workflows

because some logic ends up in tools and some in services.

Better pattern. Prefer:

```
Agents
↓
Services
↓
Tools
```

Meaning:

- agents orchestrate reasoning
- services implement business/application logic
- tools are infrastructure/utilities

For example, BETTER:

```
Agent → optimization_service → PuLP
```

Otherwise agents become giant god-objects.

3. Missing persistence/data layer

This is the largest omission. The system clearly has:

- conversations
- progress
- assessments
- spaced repetition
- competencies
- analytics

but no database layer appears. A logical architecture should show persistence.

Add something like

```mermain
subgraph Persistence["Persistence Layer"]
PG[(PostgreSQL)]
Vec[(Vector DB)]
Redis[(Redis Cache)]
end
```

Then: `Services --> Persistence`. This is essential.

Recommended revised architecture. Something closer to:

```diagram
Frontend (Streamlit)

        ↓

FastAPI Routes / Controllers

        ↓

Application Layer
(workflows/orchestrators)

        ↓

Agent Layer
(specialized agents)

        ↓

Domain Services
(progress, grading, competency)

        ↓

Infrastructure Services
(LLM, tools, vector DB, PostgreSQL)

        ↓

External Providers
(OpenAI, Gemini, Anthropic)
```

The biggest missing pieces are:

- persistence layer
- orchestration/application layer
- clearer dependency direction
- better separation between services and tools

### Deployment View

Describe the physical infrastructure on which the system runs, including servers, networks, and other resources needed to support the application. This view assigns the various software components to the infrastructure, ensuring that the system meets non-functional requirements such as availability, scalability, and performance.

### Implementation View

It details the organization of the source code and the structure of the files, packages, and dependencies in the code repository, allowing developers to understand how the software is structured to facilitate its development and maintenance.

### Data View

The Data View describes the database tables and their respective relationships.

#### Task

Each view must **include an image that graphically represents it**. Then, after the image, **the view should be described in detail, referring back to the image**.
