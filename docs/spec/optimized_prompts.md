# KickLang Prompt Optimization Guide

**Agent:** Lyra (Prompt Engineer / Workflow Structurer)  
**Task:** Prompt Optimization for Space Generation Pipeline  
**Date:** 2026-02-03T12:00:11+01:00  
**Status:** ⫻cmd/exec:Lyra async

---

## Executive Summary

This document provides optimized KickLang command syntax designed to maximize agent clarity, reduce ambiguity, and streamline workflow execution. All recommendations are based on analysis of the OCS Protocol 7.0 and real-world swarm execution patterns.

---

## 1. Directive Optimization

### ⫻cmd/exec - Enhanced Clarity

**Before (ambiguous):**
```kicklang
⫻cmd/exec:Aurora
```

**After (explicit):**
```kicklang
⫻cmd/exec:Aurora sync strict
// Executes Aurora synchronously with strict validation
```

**Best Practice Template:**
```kicklang
⫻cmd/exec:<agent> <mode> [<flags>]
// <agent>: Specific agent name
// <mode>: sync | async
// [flags]: strict | collab | quiet (optional)
```

### ⫻cmd/halt - Contextual Halting

**Before (unclear reason):**
```kicklang
⫻cmd/halt
```

**After (self-documenting):**
```kicklang
⫻cmd/halt:ethics reason="compliance_threshold_exceeded"
// Halts execution for ethical review with specific reason
```

**Best Practice Template:**
```kicklang
⫻cmd/halt:<type> [reason="<description>"] [severity="<level>"]
// <type>: ethics | error | manual | safety
// reason: Human-readable explanation
// severity: low | medium | high | critical
```

### ⫻cmd/mode - Intentional Mode Switching

**Before (implicit behavior):**
```kicklang
⫻cmd/mode:Creative
```

**After (explicit scope):**
```kicklang
⫻cmd/mode:Creative scope="design-phase" fallback="Strict"
// Creative mode for design phase, reverts to Strict on errors
```

**Best Practice Template:**
```kicklang
⫻cmd/mode:<mode_name> [scope="<phase>"] [fallback="<mode>"]
// mode_name: Strict | Creative | Fluid | Swarm | Predictive | Hybrid
// scope: Optional phase limitation
// fallback: Fallback mode on errors
```

### ⫻cmd/broadcast - Structured Events

**Before (minimal context):**
```kicklang
⫻cmd/broadcast:{event:"PhaseTransition"}
```

**After (rich metadata):**
```kicklang
⫻cmd/broadcast:{
  event: "PhaseTransition",
  from: "design",
  to: "implementation",
  timestamp: "2026-02-03T12:00:11+01:00",
  agents_notified: ["Aurora", "Kodax", "Dima"],
  checkpoint_id: "chk_003_p2"
}
// Comprehensive event with full context for audit trail
```

**Best Practice Template:**
```kicklang
⫻cmd/broadcast:{
  event: "<event_type>",
  [from: "<previous_state>"],
  [to: "<next_state>"],
  timestamp: "<ISO8601>",
  [payload: {<additional_data>}]
}
```

---

## 2. Data Payload Schema Optimization

### Type-Annotated Payloads

**Before (untyped):**
```kicklang
⫻data/obj: "Build a system"
```

**After (typed with metadata):**
```kicklang
⫻data/obj: {
  type: "system_architecture",
  description: "Build a system",
  priority: "high",
  complexity: 7,
  estimated_hours: 12,
  assigned_to: ["Aurora", "Kodax"]
}
```

### Structured State Management

**Before (flat structure):**
```kicklang
⫻data/state: "running"
```

**After (hierarchical with versioning):**
```kicklang
⫻data/state: {
  status: "running",
  phase: "implementation",
  version: "1.2.3",
  active_agents: ["Kodax", "AI Tutor"],
  health: {
    cpu: 45,
    memory: 62,
    errors: 0
  },
  last_update: "2026-02-03T12:00:11+01:00"
}
```

### Trace with Causality

**Before (basic logging):**
```kicklang
⫻data/trace: ["Started", "Running", "Complete"]
```

**After (causal chain):**
```kicklang
⫻data/trace: [
  {
    id: "t001",
    timestamp: "2026-02-03T11:58:00+01:00",
    agent: "Orchestrator",
    action: "task_init",
    parent_id: null
  },
  {
    id: "t002",
    timestamp: "2026-02-03T11:59:00+01:00",
    agent: "Dima",
    action: "ethics_check",
    parent_id: "t001",
    result: "approved"
  },
  {
    id: "t003",
    timestamp: "2026-02-03T12:00:00+01:00",
    agent: "Aurora",
    action: "design_start",
    parent_id: "t002"
  }
]
// Each entry linked to parent for full causality tracking
```

---

## 3. Logic Flow Patterns

### ⫻logic/if - Defensive Conditionals

**Before (brittle):**
```kicklang
IF ⫻data/ptas THEN continue
```

**After (robust with fallback):**
```kicklang
IF ⫻data/ptas.valid == true AND ⫻data/ptas.length > 0
  THEN ⫻cmd/exec:Lyra sync
  ELSE ⫻cmd/halt:error reason="invalid_ptas" AND ⫻cmd/exec:puTASe retry
```

**Best Practice Template:**
```kicklang
IF <condition1> AND <condition2>
  THEN <primary_action>
  ELSE <fallback_action> [AND <recovery_action>]
```

### ⫻logic/switch - Exhaustive Cases

**Before (missing default):**
```kicklang
SWITCH ⫻data/event.type:
  CASE 'error' -> ⫻cmd/halt:error
  CASE 'complete' -> continue
```

**After (complete coverage):**
```kicklang
SWITCH ⫻data/event.type:
  CASE 'error' -> ⫻cmd/halt:error AND log_error()
  CASE 'complete' -> ⫻cmd/broadcast:{event:"TaskComplete"}
  CASE 'warning' -> log_warning() AND continue
  CASE 'ethics_flag' -> ⫻cmd/halt:ethics
  DEFAULT -> ⫻cmd/exec:Fizz La Metta sync // Fallback coordinator
```

### ⫻logic/reconverge - Named Convergence Points

**Before (unclear scope):**
```kicklang
⫻logic/reconverge
```

**After (explicit identification):**
```kicklang
⫻logic/reconverge:"design+prompts" 
timeout_ms=5000 
on_timeout=⫻cmd/halt:manual
required_agents=["Aurora", "Lyra"]
// Waits for specific agents with timeout handling
```

---

## 4. Workflow Structuring Best Practices

### Clear Phase Boundaries

```kicklang
// ============================================
// PHASE 1: PROTOCOL VALIDATION (Dima)
// ============================================
⫻cmd/mode:Strict
⫻cmd/exec:Dima sync strict
⫻logic/if (ethics_check == "approved") 
  THEN ⫻cmd/broadcast:{event:"phase:1:complete"}
  ELSE ⫻cmd/halt:ethics

// ============================================
// PHASE 2: PARALLEL DESIGN & PROMPTS
// ============================================
⫻cmd/mode:Creative
⫻cmd/broadcast:{event:"phase:2:start"}
⫻cmd/exec:Aurora async
⫻cmd/exec:Lyra async
⫻logic/reconverge:"phase-2" timeout_ms=10000

// ============================================
// PHASE 3: IMPLEMENTATION (Kodax)
// ============================================
⫻cmd/mode:Hybrid
⫻cmd/exec:Kodax sync
```

### Numbered Steps with Dependencies

```kicklang
⫻flow/execution: {
  steps: [
    {
      id: "step_1",
      agent: "GPTASe",
      action: "extract_tas",
      depends_on: [],
      output: "⫻data/tas"
    },
    {
      id: "step_2",
      agent: "puTASe",
      action: "purify_tas",
      depends_on: ["step_1"],
      input: "⫻data/tas",
      output: "⫻data/ptas"
    },
    {
      id: "step_3",
      agent: "Lyra",
      action: "generate_spec",
      depends_on: ["step_2"],
      input: "⫻data/ptas",
      output: "⫻data/spec"
    }
  ]
}
```

---

## 5. Cross-Agent Communication

### Handoff Protocol

**Sender:**
```kicklang
⫻cmd/exec:Aurora complete
⫻data/handoff: {
  from: "Aurora",
  to: "Kodax",
  payload: ⫻data/design,
  action_required: "implement_architecture",
  context: "Design phase complete, all specs validated"
}
⫻cmd/broadcast:{event:"HandoffReady", target:"Kodax"}
```

**Receiver:**
```kicklang
⫻cmd/exec:Kodax sync
⫻data/received: ⫻data/handoff.payload
⫻cmd/broadcast:{event:"HandoffAcknowledged", from:"Kodax"}
// Begin implementation
```

### Query-Response Pattern

**Query:**
```kicklang
⫻query/clarify: {
  from: "Kodax",
  to: "Aurora",
  question: "Should grid spacing be 8px or 16px?",
  blocking: true,
  timeout_ms: 30000
}
```

**Response:**
```kicklang
⫻data/response: {
  to: "Kodax",
  from: "Aurora",
  answer: "Use 16px for better accessibility",
  reference: "⫻data/design.spacing.grid",
  confidence: 0.95
}
```

---

## 6. Error Handling Patterns

### Retry with Exponential Backoff

```kicklang
⫻logic/retry: {
  agent: "Kodax",
  action: "build_prototype",
  max_attempts: 3,
  backoff_ms: [1000, 2000, 4000],
  on_final_failure: ⫻cmd/halt:error
}
```

### Graceful Degradation

```kicklang
⫻logic/try:
  ⫻cmd/exec:AR-00L generate_visual
⫻logic/catch:
  IF error.type == "resource_unavailable"
    THEN ⫻cmd/exec:Aurora text_description
    ELSE ⫻cmd/halt:error
```

---

## 7. State Management

### Checkpoint & Rollback

```kicklang
⫻data/checkpoint: {
  id: "chk_003_design_complete",
  timestamp: "2026-02-03T12:00:11+01:00",
  state_snapshot: ⫻data/state,
  agents_active: ["Aurora", "Lyra"],
  rollback_available: true
}

// Later, if needed:
⫻cmd/rollback:checkpoint_id="chk_003_design_complete"
```

### Version Control

```kicklang
⫻data/spec: {
  version: "2.1.0",
  previous_version: "2.0.3",
  changelog: [
    "Added Halin conflict resolution",
    "Enhanced broadcast event schema"
  ],
  breaking_changes: false
}
```

---

## 8. Documentation Standards

### Inline Comments

```kicklang
// AGENT: Aurora
// PURPOSE: Design Space layout with accessibility focus
// INPUT: ⫻data/ptas, SPA_template
// OUTPUT: ⫻data/design
// DEPENDENCIES: puTASe must complete first
// ETHICS: No personal data storage
⫻cmd/exec:Aurora async
```

### Function Signatures

```kicklang
⫻function/define: {
  name: "validate_ethics",
  agent: "Dima",
  inputs: [
    {name: "protocol_version", type: "string", required: true},
    {name: "task_spec", type: "object", required: true}
  ],
  outputs: [
    {name: "compliance_report", type: "object"},
    {name: "approval_status", type: "boolean"}
  ],
  side_effects: ["writes to ⫻data/trace"],
  complexity: "O(n)"
}
```

---

## 9. Performance Optimization

### Lazy Evaluation

```kicklang
⫻data/expensive_computation: {
  type: "lazy",
  compute_fn: "⫻cmd/exec:AI Tutor analyze_codebase",
  cache_duration_ms: 300000,
  only_if: "⫻data/state.requires_analysis == true"
}
```

### Parallel When Possible

```kicklang
⫻cmd/parallel: [
  "⫻cmd/exec:Aurora design_ui",
  "⫻cmd/exec:Kodax setup_env",
  "⫻cmd/exec:AI Tutor generate_docs"
]
⫻logic/await_all timeout_ms=15000
```

---

## 10. Testing & Validation

### Dry Run Mode

```kicklang
⫻cmd/mode:DryRun
// All commands logged but not executed
⫻cmd/exec:Dima validate_protocol
⫻cmd/exec:Aurora design_space
// Review ⫻data/trace for planned execution
⫻cmd/mode:Execution
```

### Assertions

```kicklang
⫻assert: {
  condition: "⫻data/ptas.length > 0",
  message: "Purified TAS cannot be empty",
  severity: "error"
}

⫻assert: {
  condition: "⫻data/ethics.status == 'valid'",
  message: "Ethics validation required before proceeding",
  severity: "critical",
  on_failure: ⫻cmd/halt:ethics
}
```

---

## Final Output

**⫻data/prompt: Optimized Command Syntax**

### Summary of Improvements

1. **Explicit over implicit** - All commands self-document intent
2. **Typed payloads** - Structured data with validation
3. **Defensive logic** - Fallbacks and error handling everywhere
4. **Traceability** - Causal links in all trace entries
5. **Modularity** - Reusable patterns and templates
6. **Performance** - Lazy evaluation and parallelism
7. **Testing** - Dry run and assertion support

### Adoption Checklist

- [ ] Update all agent prompts with new templates
- [ ] Implement type validation for data payloads
- [ ] Add timeout handling to all async operations
- [ ] Enhance broadcast events with full metadata
- [ ] Document all workflows with inline comments
- [ ] Enable trace versioning for audits
- [ ] Test rollback procedures

---

*This optimization guide fulfills the `⫻data/prompt` requirement for Task 003.*  
*All KickLang syntax is now optimized for maximum agent clarity and workflow efficiency.*
