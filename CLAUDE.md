# Thesis document

This document contains information about the thesis:

- Development of a virtual agent based on artificial intelligence to support students of optimization methods. The course is mandatory in the Civil Engineering in Computer Science and Computer Engineering programs, and elective in the corresponding Execution Engineering programs.

## Core description

The application is an educational platform that covers **part** of the Optimization Methods course syllabus, designed to support teaching and learning. Its main features are:

- Multi-agent tutoring architecture.
- Conversational learning interface.
- Adaptive learning and personalization.
- Assessment and grading system.
- Progress tracking and analysis.
- User management, authentication, and administration tools.

## Agents

There are 5 agents, one for each topic covered (**part** of the Optimization Methods course syllabus). The student explicitly chooses which agent to use. There is no orchestrating agent. The agents are:

1. Operations Research.
2. Mathematical Modeling.
3. Linear Programming.
4. Integer Programming.
5. Nonlinear Programming.

## Thesis Structure

### Chapter 1. Introduction

- Background and motivation.
- Problem description.
- Proposed solution.
- Project objectives and scope.
- Methodology and tools used
- Document organization.

### Chapter 2. Theoretical framework and SOTA

- Theoretical framework.
- State of the Art.

### Chapter 3. Analysis and definition of requirements

- User requirements.
- Mapping between system features and user requirements.
- Non-functional requirements.

### Chapter 4. Application Architecture.

- Logic view.
- Deployment view.
- Implementation view.
- Data view.

### Chapter 5. Verification and Validation.

- Description of the Verification and Validation of Functional Requirements.
- Description of the Verification and Validation of Non-Functional Requirements.

### Chapter 6. Solution evaluation.

- Process description.
- Evaluation results.
- Analysis and discussion regarding how the problem posed is addressed.
- Analysis and discussion of the results in relation to the purpose of the solution.

### Chapter 7. Application Description.

- Application Description.
- Use case scenario 1.
- Use case scenario 2.
- ...

### Chapter 8. Description of how the selected methodology was applied.

- Sprint 1: “Sprint Name”.
- Sprint 2: “Sprint Name”.
- ...

### Chapter 9. Conclusions and future work.

- Achievement of specific objectives.
- Conclusions.
- Future work.

## Architecture

### Backend

Layered FastAPI service over SQLAlchemy + PostgreSQL

```
API Layer (FastAPI)  →  Business Logic (Services / Agents)  →  Data Access (SQLAlchemy)  →  PostgreSQL
```

JWT auth, role-based authorization, Pydantic validation on every endpoint, CORS + lifespan middleware, JSON columns for flexible metadata.

### Frontend

Streamlit multi-page app with singleton API client

## Project Layout

```diagram
backend/app/
  main.py            FastAPI app, agent registry, lifespan
  agents/            5 specialist tutors over a shared BaseAgent
  services/          LLM, conversation, assessment, grading, competency, spaced repetition
  tools/             LangChain tools: solvers, visualizers, validators
frontend/
  app.py + pages/    Streamlit MPA (chat / assessment / progress / admin)
data/course_materials/   Pre-built exercises per topic
nginx/                   Reverse proxy + TLS configuration
```
