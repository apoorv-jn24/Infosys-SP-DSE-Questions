# Technical Interview + HR Prep

## Technical interview — question bank by area

### DSA (asked of both SP and DSE candidates)
- Explain the time/space complexity of the solution you just wrote — be ready to justify it, not just state it.
- Given a problem, walk through why you chose one data structure over another (e.g., "why a hash map here and not a sorted array").
- Follow-up optimization questions: "can you do this in O(n) instead of O(n log n)?"

### OOP
- The four pillars (encapsulation, abstraction, inheritance, polymorphism) — but expect them applied to a scenario, not recited as definitions.
- Design a small class hierarchy for a given scenario (common: vehicle types, employee types, shape hierarchies) and justify your design choices.

### SQL
- Joins (inner/left/right/full), aggregations with GROUP BY/HAVING, subqueries vs. joins tradeoffs.
- Window functions if you're going for DSE — increasingly common in recent interviews.
- Cross-reference your `sql-notes-repo` for the deeper interview-question set you already built there.

### System design (lighter weight, mostly for DSE)
- Basic API design: "design a simple endpoint for X" — expect to sketch request/response shape, not a full distributed system.
- Database schema design for a small, familiar domain (e.g., a library system, an e-commerce cart).

### Resume-based (very heavily weighted — treat as equal priority to DSA)
Go through **every project and skill on your resume** and prepare answers for:
- Walk me through your final year project, end to end.
- What was the most challenging problem you solved in it?
- Which technology did you use for the backend/frontend, and why that over the alternatives?
- What's the time complexity of the key algorithm in your project?
- If you had to redesign this project from scratch, what would you change?
- For any framework listed on your resume (e.g., FastAPI): be ready to write a basic GET and POST endpoint live — this is a real, recently-asked DSE interview question.
- What version control system did you use, and describe your actual Git workflow (branching strategy, how you handle merge conflicts) — not just command definitions.

**Rule of thumb**: know every bullet on your resume well enough that you could be asked to defend it for five minutes straight.

## HR / behavioral round

- "Why Infosys" — have a genuine, specific answer (not generic "great company culture").
- Standard behavioral prompts: a time you disagreed with a teammate, a time you missed a deadline, how you handle ambiguous requirements.
- Situational judgment style questions — if you want the same style of prep you used for TCS IPA's BizSkills section, treat this the same way: reason through the most "professionally sound" response, not necessarily the most literal one.
- Know your resume's timeline cold: gaps, certifications, internship dates — HR rounds often probe consistency.

## Interview-day logistics

- Environment: confirm whether the technical round is virtual (have your IDE/compiler ready, test your camera/mic) or in-person.
- Have 2–3 thoughtful questions ready to ask the interviewer at the end — about the specific team/role, not generic questions answerable from the company website.
