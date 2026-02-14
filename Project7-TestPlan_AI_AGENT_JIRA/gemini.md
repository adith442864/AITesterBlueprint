# 📜 Project Constitution - gemini.md

> **Project:** TestPlan AI Agent JIRA Integration  
> **Status:** Phase 0 - Draft  
> **Last Updated:** 2026-02-14

---

## 🏛️ Architectural Invariants

These rules must never be violated:

1. **Reliability Over Speed:** All automation must be deterministic and self-healing
2. **3-Layer Architecture:** Strict separation between Architecture, Navigation, and Tools
3. **Data-First:** JSON schemas must be defined before any code is written
4. **No Guessing:** Business logic must be explicitly defined, never assumed

---

## 📊 Data Schemas

*To be defined during Phase 1 after Discovery Questions are answered*

### Input Schema
```json
{
  "TBD": "To be defined"
}
```

### Output Schema
```json
{
  "TBD": "To be defined"
}
```

---

## 🎭 Behavioral Rules

### System Personality
- Professional and concise
- Prioritizes clarity over cleverness
- Validates all assumptions

### Do Not Rules
- Do NOT write scripts in `tools/` before Discovery is complete
- Do NOT assume business logic without confirmation
- Do NOT skip the handshake verification in Phase 2

### Tone Guidelines
- Clear, technical communication
- Proactive error reporting
- Transparent about limitations

---

## 🔌 Integration Requirements

*To be populated based on Discovery Questions*

| Service | Purpose | Credentials Status |
|---------|---------|-------------------|
| JIRA | TBD | TBD |

---

## 📁 Directory Structure

```
Project7-TestPlan_AI_AGENT_JIRA/
├── BLAST.md              # Framework reference
├── gemini.md             # Project Constitution (this file)
├── task_plan.md          # Phases and checklists
├── findings.md           # Research and discoveries
├── progress.md           # Activity log
├── architecture/         # Layer 1: Technical SOPs
├── tools/                # Layer 3: Python scripts
└── .tmp/                 # Intermediate files
```

---

## ✅ Approval Checklist

- [ ] Discovery Questions answered
- [ ] Data schemas defined
- [ ] Blueprint approved
- [ ] Ready to proceed to Phase 2
