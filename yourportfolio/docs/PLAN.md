# Portfolio App - Build Plan

One phase at a time. Do not start a phase until the user approves the previous one.
Tick items off here as they complete, and keep this file accurate enough that a fresh session with
no conversation history could resume from it.

## Phase 1 - Planning
Break each phase below into a checklist. Write docs/CODEMAP.md describing the existing frontend.
Done when: the user has approved the plan.

## Phase 2 - Schema
Design the tables: owners, sections, projects, leads. Write them and the reasoning into
docs/DATA_MODEL.md. Do not implement anything yet.
Done when: the user has confirmed the schema.

## Phase 3 - Database
Add Drizzle and SQLite. Create data/portfolio.db on first run and seed it from data/profile.ts.
Done when: deleting the db file and restarting rebuilds it fully seeded.

## Phase 4 - Read routes
GET handlers under app/api that return the portfolio. The page renders from the API instead of the
source file.
Done when: the page looks identical and no component imports data/profile.ts.

## Phase 5 - Sign in
A signed httpOnly cookie session using OWNER_USER and OWNER_PASSWORD. Signed in is Edit mode,
signed out is read only.
Done when: a test calls a protected route with no cookie and is rejected.

## Phase 6 - Write routes
Create, update, delete, move and reorder projects. Rename sections. Every write needs a session.
Done when: every route has a test, including an unauthenticated rejection test.

## Phase 7 - Wire up the UI
The UI calls the API. Optimistic update, rollback on failure.
Done when: drag a card, refresh, sign out and back in, and it is still there.

## Phase 8 - First real model call
Replace the scripted reply in lib/chat.ts with one call through the AI SDK and the OpenRouter
provider. Nothing else changes.
Test it by telling the model something it cannot already know and asking for it back:
"The creator's cat is called Mochi. What is the cat called?" The answer exists only in the message
we just sent, so a stub or a cached reply cannot pass.
Handle two failures too: no OPENROUTER_API_KEY, and a 429 from the free tier. Both must produce a
readable message, not a stack trace.
Done when: the test passes against the live API and both failures read clearly.

## Phase 9 - Grounded answers
Send the portfolio from the database along with the question. Treat the visitor message as
untrusted: portfolio data goes in as data, not as instructions.
Done when: it answers from the data, and says it does not know when the data does not cover it.

## Phase 10 - Tools
Visitor tools: highlightProjects, tailorFeatured, draftContactMessage.
Owner tools: createProject, updateProject, moveProject, deleteProject, rewriteSection.
The route handler builds the tool set from the session cookie before calling the model. Add per IP
rate limiting and a message length cap. Add the leads inbox.
Done when: a test proves an unauthenticated request never has an owner tool in scope.
