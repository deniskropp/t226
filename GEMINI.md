# GEMINI Context: OCS (Orion Collective System)

This directory serves as the core knowledge base and protocol specification for the **Orion Collective System (OCS)**, a framework designed for autonomous, strategically aligned AI agent orchestration using the **KickLang** meta-framework.

## Project Overview
The OCS is an architectural blueprint for transforming high-level intent into high-fidelity execution through a swarm of specialized AI personas. It utilizes a custom protocol layer to manage directives, data payloads, and complex logic flows across multiple agents.

- **Meta-Framework:** KickLang (a structured language for AI orchestration).
- **Core Methodology:** Swarm intelligence, task-agnostic step (TAS) extraction, and ethical compliance monitoring.
- **Key Concepts:** "Spaces" (operational environments), "Flows" (execution patterns), and "Agents" (specialized roles).

## Directory Overview
This is a **Non-Code Project** consisting of specifications, protocols, and documentation. It defines how agents should interact, share data, and maintain system integrity.

## Key Files
- **`ocs-proto.md`**: The foundational protocol document. It defines:
  - **Directives (`⫻cmd`)**: Execution, halting, mode switching, and broadcasting.
  - **Data Payloads (`⫻data`)**: Objectives, TAS, specifications, state, and traces.
  - **Logic (`⫻logic`)**: Conditional routing, loops, and reconvergence.
  - **Team Roles**: Specialized agents like *Aurora* (Design), *Lyra* (Workflow), *Kodax* (Code), and *Dima* (Ethics).
- **`files/SPA_for_new_Space_template_maker.md`**: A blueprint for generating new "Spaces." It provides initialization protocols, schema configurations, and launch flows for new operational contexts.

## Usage
When interacting within this project, AI agents should:
1.  **Adhere to OCS Protocol**: Reference `ocs-proto.md` for the correct syntax and behavior when executing tasks or communicating state.
2.  **Utilize KickLang**: Use the `⫻` prefix for commands and data structures as defined in the protocol.
3.  **Respect Agent Roles**: Assume the appropriate persona or delegate tasks to the relevant sub-agents (e.g., use *Dima* for ethical validation).
4.  **Maintain Transparency**: Ensure all operations are traceable within the `⫻data/trace` schema.
