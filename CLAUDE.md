# CLAUDE.md - Project Instructions

This file provides Claude Code with context about the project structure and coding standards.

## Build flow

Features follow the global build flow in `~/.claude/CLAUDE.md`: grill → `to-spec` → `to-tickets` → `implement` → `code-review` → `pr` → `retro`. New or redesigned UI goes through the `mobbin` skill. David's Pipeline (`/spec-init`, `/spec-expand`, `/auto-build`, `/phase-gate`, `/ship`) and its role agents are retired; plans under `docs/plans/` and `docs/superpowers/` are history, not instructions.

---

## Prompt Structure

When giving tasks to Claude, use this format for best results:

**Context:** Background info, feature goal, libraries to use
**Task:** What to do, reference specific files/docs
**Constraints:** What NOT to do (prevent over-engineering)

### Example Prompt

```
Context: We're building a user dashboard. Using React + Tailwind. The auth system is already set up in src/auth/.

Task: Add a "last login" timestamp to the user profile card in src/components/ProfileCard.tsx

Constraints: Don't refactor existing code. Don't add new dependencies. Keep it simple.
```

---

## Coding Standards

- **Type Safety**: Never use `any` types. Always define proper interfaces.
- **Error Handling**: Always handle errors gracefully with informative messages.
- **Security**: Validate all inputs. Never expose secrets. Follow OWASP guidelines.
- **Performance**: Avoid N+1 queries. Use appropriate caching strategies.
- **Testing**: Write tests for critical paths. Cover edge cases.

---

## Safety Rules

- Never commit `.env` files or secrets
- Always validate user input
- Use parameterized queries for database operations
- Follow the principle of least privilege
- Review security implications before deploying

---

## Notes

- This setup works with any modern web stack
- All agents read this file for project context
