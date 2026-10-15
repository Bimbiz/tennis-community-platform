# Amateur Tennis Community Platform

## Project Overview

**Project Title:** Development of a Mobile Application for the Amateur Tennis Community with Automatic Rating Calculation and Matching of Pairs

This diploma project focuses on the design and development of a cross-platform mobile application for amateur tennis players and tournament organizers.

The platform aims to simplify tournament organization, player registration, opponent and partner matching, match result management, and automatic player rating calculation.

## Problem Statement

Amateur tennis players often rely on messaging groups and informal communication to find tournaments, partners, and opponents. These methods may lack structured tournament management, consistent player skill assessment, and automated matchmaking.

The proposed platform aims to address these limitations through centralized tournament management and a rating-based matchmaking system.

## Target Users

- Amateur tennis players
- Tennis tournament organizers
- Local tennis communities and clubs

## Project Team

| Team Member | Group | Responsibility |
|---|---|---|
| Timur Bizinskiy | SE-2412 | Mobile Development — Flutter/Dart |
| Arlan Tulegenov | SE-2429 | Backend Development — Python/FastAPI |

**Academic Supervisor:** Zhibek Sarsenova, Senior Lecturer

## Project Scope

The planned system includes:

- User registration, authentication, and player profiles
- Tournament creation and management
- Singles and Doubles tournament formats
- Individual and premade-team registration
- Automatic doubles partner formation
- Tournament scheduling and match management
- Match result submission and confirmation
- Internal player rating based on Elo or Glicko-2
- NTRP-inspired displayed player levels
- Player statistics and match history

Additional tournament formats, notification services, and other advanced features are subject to scope prioritization.

Detailed scope and requirements are maintained in the project documentation.

## Technology Stack

| Component | Technology |
|---|---|
| Mobile Application | Flutter, Dart |
| Backend | Python, FastAPI |
| Architecture | Modular Monolith |
| Database | PostgreSQL (under evaluation) |
| API | REST, JSON, OpenAPI |
| Local Storage | Drift / SQLite (under evaluation) |
| Rating Algorithm | Elo / Glicko-2 (under evaluation) |
| UI/UX Prototyping | Figma |
| Version Control | Git, GitHub |
| Project Management | YouTrack |

## Project Status

**Current Stage:** Research, requirements analysis, architecture design, and project planning.

The project is currently in the pre-development stage. The initial focus is on defining requirements, evaluating technologies, preparing architectural diagrams, and designing a mobile application prototype.

A complete application implementation is not required for the first pre-defence.

## Repository Structure

- `src/mobile/` - Flutter application
- `src/backend/` - FastAPI application
- `docs/proposal` - project proposal and scope documentation
- `docs/literature-review/` - scientific literature review
- `docs/comparisons/` - existing systems and technology comparisons
- `docs/requirements/` - functional and non-functional requirements
- `docs/architecture/` - architectural diagrams and editable source files
- `docs/prototype/` - UX/UI prototype materials
- `docs/project-management/` - milestones, risks, and project planning
- `tests/` - shared and integration testing materials
- `config/` - configuration templates

## Project Documentation

All project documentation is maintained in the [`docs/`](docs/) directory.

## Project Management

**YouTrack Project:** [Amateur Tennis Community](https://amateur-tennis-app.youtrack.cloud)

Tasks are tracked in YouTrack and linked to Git branches, commits, and pull requests.

Git branches, commits, and pull requests reference
the corresponding YouTrack issue IDs (ATC-XX).

## Development Workflow

1. Select an assigned YouTrack issue.
2. Create a dedicated feature branch using the issue ID.
3. Implement and test the required changes.
4. Commit changes with the corresponding YouTrack issue ID.
5. Open a pull request referencing the issue.
6. Request code review from another team member.
7. Merge the approved changes into `main`.
8. Update the YouTrack issue status.

## Setup and Testing

Application setup, execution, and testing instructions will be added as the mobile and backend implementations become available.