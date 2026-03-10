# BMad Method Quick Reference Card

## 🛠️ Essential Commands

### Installation
```bash
npx bmad-method install
# When prompted, select: BMad Method
```

### BMad Slash Commands (in Copilot Chat)

| Command | Agent | Purpose |
|---------|-------|---------|
| `/bmad-help` | Any | Your intelligent guide — ask anything! |
| `/bmad-pm` | PM | Invoke Product Manager agent |
| `/bmad-create-prd` | PM | Create Product Requirements Document |
| `/bmad-architect` | Architect | Invoke Architect agent |
| `/bmad-create-architecture` | Architect | Create architecture document |
| `/bmad-create-epics-and-stories` | PM | Break down PRD into epics |
| `/bmad-sm` | SM | Invoke Scrum Master agent |
| `/bmad-sprint-planning` | SM | Initialize sprint tracking |
| `/bmad-create-story` | SM | Create a story file |
| `/bmad-dev-story` | DEV | Implement a story |
| `/bmad-code-review` | DEV | Review implemented code |

### Copilot Chat Shortcuts

| Shortcut | Action |
|----------|--------|
| `Ctrl+Shift+I` (Win) / `Cmd+Shift+I` (Mac) | Open Copilot Chat |
| Open new chat tab | Start a fresh context for each workflow |

> ⚠️ **Key Rule:** Each BMad workflow should run in its own **fresh chat session**.

---

## 🔄 The 4-Phase Workflow

### 1️⃣ Analysis Phase
**Commands:** `/bmad-pm` → `/bmad-create-prd`  
**Agent:** Product Manager (PM)  
**Output:** PRD saved to `_bmad-output/`  
**Contains:** Features, User Stories, Success Criteria

### 2️⃣ Planning Phase
**Commands:** `/bmad-architect` → `/bmad-create-architecture` → `/bmad-create-epics-and-stories`  
**Agent:** Architect  
**Output:** Architecture document + ADRs in `_bmad-output/`  
**Contains:** Component structure, Tech stack, Decision records, Epics & Stories

### 3️⃣ Story Preparation Phase
**Commands:** `/bmad-sm` → `/bmad-sprint-planning` (first time) → `/bmad-create-story`  
**Agent:** Scrum Master (SM)  
**Output:** Story file ready for implementation  
**Contains:** Implementation plan, acceptance criteria

### 4️⃣ Implementation Phase
**Commands:** `/bmad-dev-story` (in a new chat)  
**Agent:** Developer (DEV)  
**Output:** Component files + tests  
**Contains:** Working code, unit tests

---

## 📁 File Structure

```
your-project/
├── _bmad/                     # BMad configuration
│   └── bmm/                   # BMad Method module
│       ├── agents/            # Agent definitions
│       ├── workflows/         # Workflow definitions
│       └── tasks/             # Task definitions
├── _bmad-output/              # Generated artifacts
│   ├── prd.md                 # Product Requirements (generated)
│   ├── architecture.md        # Technical design (generated)
│   └── stories/               # Story files (generated)
└── src/
    ├── components/            # Your components (generated)
    └── App.tsx                # Main app file
```

---

## 📝 Agent Question Tips

### Product Manager Agent (`/bmad-pm`)
- **Keep answers short** (1-2 sentences)
- **Accept defaults** when suggested
- **Be specific** about core features
- **Avoid scope creep** (no login, databases, etc.)

### Architect Agent (`/bmad-architect`)
- **Trust the suggestions** (they're based on best practices)
- **Choose simple options** (Context over Redux, LocalStorage over DB)
- **Ask for explanations** if confused

### Developer Agent (`/bmad-dev-story`)
- **Pick clear component names** (AddTodoForm, not Form1)
- **Request validation** when needed
- **Ask for tests** to be included
- **Review code** before accepting

---

## ⚡ Speed Tips

### Faster PRD Creation
```
# Open a new chat, then:
/bmad-pm
/bmad-create-prd

# When asked for features, give complete list:
"Features: add tasks, mark complete, delete tasks, view list"

# When asked about users:
"Individual users tracking personal tasks"

# When asked about scope:
"Keep it simple - no auth or cloud sync"
```

### Faster Architecture
```
# Open a new chat, then:
/bmad-architect
/bmad-create-architecture

# Quick answers:
"Use React Context, LocalStorage, and TailwindCSS"

# Then create epics and stories:
/bmad-create-epics-and-stories
```

### Faster Story Implementation
```
# Open a new chat, then:
/bmad-sm
/bmad-sprint-planning   # first time only
/bmad-create-story      # select story 1

# Open another new chat, then:
/bmad-dev-story
# Component name: AddTodoForm
# Additional requirements: "Validate input, clear after submit, include tests"
```

---

## 🔴 Common Issues

### Issue: "Slash commands not working"
**Fix:** Restart VS Code, verify `_bmad/` folder exists, then try `/bmad-help`

### Issue: PM agent loops same question
**Fix:** Open a **fresh chat**, then `/bmad-pm` and `/bmad-create-prd`

### Issue: "Can't find PRD file"
**Fix:** Verify PRD exists in `_bmad-output/`, start fresh chat with `/bmad-architect`

### Issue: TypeScript errors in generated code
**Fix:** Check if `npm run dev` works - if yes, ignore red squiggles

### Issue: Component doesn't render
**Fix:** Check `App.tsx` has import and `<ComponentName />` tag

---

## 🎯 Success Checklist

### After Exercise 1 (Installation)
- [ ] `_bmad/` folder exists
- [ ] `_bmad-output/` folder exists
- [ ] `/bmad-help` shows intelligent guide response

### After Exercise 2 (PRD)
- [ ] PRD file exists in `_bmad-output/`
- [ ] Contains 3+ user stories
- [ ] Stories follow: "As a [role], I want [feature] so that [benefit]"

### After Exercise 3 (Architecture)
- [ ] Architecture document exists in `_bmad-output/`
- [ ] Contains component diagram
- [ ] ADRs included in architecture document
- [ ] Epics and stories created

### After Exercise 4 (Implementation)
- [ ] Component `.tsx` file created
- [ ] Test file `.test.tsx` created
- [ ] `npm run dev` works
- [ ] Component renders in browser

---

## 💡 Key Concepts

### Context Engineering
**Documents create shared understanding between agents.**

PM creates PRD → Architect reads PRD → Developer reads both

Better context = better code generation

### Architecture Decision Records (ADRs)
**Document important technical choices.**

Format:
- **Context:** Why did we need to decide?
- **Decision:** What did we choose?
- **Consequences:** What are the trade-offs?

### Agent Roles
- **PM:** Business requirements, user stories (`/bmad-pm`)
- **Architect:** Technical design, component structure (`/bmad-architect`)
- **SM:** Sprint planning, story creation (`/bmad-sm`)
- **Developer:** Code generation, implementation (`/bmad-dev-story`)

### Fresh Chat Per Workflow
BMad V6 works best when each workflow runs in a **new chat session**. This prevents context pollution and ensures agents start fresh with the right context.

---

## 🚀 Next Steps

### Complete Your App
```bash
# Implement remaining stories (each in a fresh chat)

# Story 2: Mark complete
/bmad-sm
/bmad-create-story   # select story 2
# Then in new chat:
/bmad-dev-story

# Story 3: Delete tasks
/bmad-sm
/bmad-create-story   # select story 3
# Then in new chat:
/bmad-dev-story
```

### Add Features
```bash
# 1. Update PRD with new feature (fresh chat)
/bmad-pm → /bmad-create-prd
# 2. Update architecture (fresh chat)
/bmad-architect → /bmad-create-architecture
# 3. Create user story (fresh chat)
/bmad-sm → /bmad-create-story
# 4. Implement (fresh chat)
/bmad-dev-story
```

### Learn More
- Watch: [BMad Masterclass](https://www.youtube.com/watch?v=LorEJPrALcg) (42 min)
- Read: [BMad Docs](https://docs.bmad-method.org/)
- Join: BMad Discord community

---

## 📞 Emergency Help

**During Workshop:**
- Ask facilitator in breakout room
- Share screen for debugging
- Request backup files

**After Workshop:**
- Review recording
- Join BMad Discord
- Email workshop organizer

---

**Pro Tip:** Save this reference card - you'll use it for every BMad project!

**Remember:** The goal is learning the workflow, not perfect code. Even experienced devs hit issues. Keep practicing! 🚀