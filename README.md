# Kanban Cloud Portfolio

A practical cloud engineering portfolio project built around PLANKA.

The project begins as a local Docker Compose deployment and will evolve into a cloud-hosted platform. The purpose is to demonstrate infrastructure engineering against a real workload rather than a disposable lab.

## Why This Exists

My partner and I needed a simple way to track projects, maintenance and improvements in our apartment.
We tried notepads but they got lost. Note apps got cluttered and disorganised quickly. Nothing seemed to work. Then one day at work during team standup it struck me; we could use a kanban board!

Tools like Jira have free-tier licensing but that is designed for corporate workloads and I didn't want to create a barrier to entry for my partner who is non-technical. So I did a bit of research and soon discovered PLANKA.
I liked the simple UI and the idea of a self-hosted projects board appealed to me. The more I thought about it though the more I saw it as a possibility to exhibit the cloud skills I have developed over the last 8 years of working in the tech industry.
That's how we got to where it is today.

I hope this is something you can use for yourself. It's simple to setup and the applications are endless. All credit to the PLANKA, Docker and PostgreSQL teams for making something like this possible.


## Project Status

**Current phase:** Local containerised deployment

The application is running successfully on Docker Desktop through WSL2. PLANKA is accessible across the local network and persistent application state survives container recreation.

## Current Architecture

```text
LAN Client
    |
    | HTTP :3000
    v
Windows Host
    |
    v
Docker Desktop
    |
    +------------------------+
    |                        |
    v                        v
PLANKA                  PostgreSQL
:1337                       :5432
    |                        |
    v                        v
planka-data            postgres-data
```

PLANKA and PostgreSQL communicate over the internal Docker Compose network.

Only the PLANKA application port is published to the host. PostgreSQL is not exposed to the LAN.

## Technology

| Component | Implementation |
| --- | --- |
| Application | PLANKA 2.2.1 |
| Database | PostgreSQL 16 Alpine |
| Container Runtime | Docker Desktop |
| Orchestration | Docker Compose |
| Linux Environment | WSL2 |
| Persistent Storage | Docker named volumes |
| Source Control | Git and GitHub |

## Current Implementation

The local deployment currently includes:

- PLANKA pinned to a specific application release
- PostgreSQL pinned to major version 16
- Environment-based runtime configuration
- Authenticated PostgreSQL connectivity
- Separate persistent volumes for application and database data
- PostgreSQL health checks
- Dependency-aware PLANKA startup
- Automatic container restart policies
- LAN access to the PLANKA web interface
- Secrets excluded from version control

## Configuration

Runtime configuration is supplied through environment variables.

Local secrets are stored in:

```text
.env
```

This file is intentionally excluded from version control.

The Compose configuration references these values at runtime rather than storing credentials directly in the repository.

## Repository Structure

```text
.
├── compose.yaml
├── .gitignore
└── README.md
```

This structure will expand as cloud infrastructure and automation are introduced.

## Roadmap

The next stages of the project will move the workload from a local Docker environment into the cloud.

Planned work includes:

- Infrastructure as code
- Cloud networking
- Automated host configuration
- DNS and TLS
- Backup and recovery
- Monitoring and alerting
- Centralised logging
- Security hardening
- CI/CD
- Vulnerability scanning
- Disaster recovery testing

## Objective

The final goal is a production-style cloud deployment that demonstrates the design, deployment, security and operation of a persistent containerised application.

PLANKA provides the workload. The portfolio focus is the infrastructure and operational engineering around it.