# Bindery patch — July 6, 2026
Applied directly to the deployed bundle (index-BsbE9ke_.js). Full details in chat.

STYLE / AUDIENCE FIDELITY
1. Prose engine no longer hardcoded to "dense publishable fiction" — style guide + charter now decide audience, reading level, vocabulary, sentence length.
2. Craft Laws demoted to "defaults for adult fiction"; style guide explicitly outranks them. Children's-book exception written in (named emotions OK, short concrete sentences, no subtext technique).
3. Dialogue-length law (8–20 turns) now scales to audience.
4. STYLE GUIDE block is always sent, promoted to "highest authority," with an inference fallback when no style notes were given (this was the empty-styleGuide path that produced adult prose for kids' briefs).
5. Charter builder must open the styleGuide by naming audience + reading level with hard numbers, and list 3–4 concrete habits when an author is named. Audience/age constraints copied word-for-word into the charter.
6. Verifier now receives the style guide and returns "styleBreaks" (quoted violations); these feed revision directives, so off-register prose gets caught and rewritten automatically.

ANTI-AI-TROPE
7. New Craft Law 9: bans "not X but Y," rule-of-three stacks, tapestry/testament/palpable, "a beat passed," breath-she-didn't-know clichés, em-dash overuse, uniform sentence lengths, self-explaining images.
8. Verifier's styleBreaks also flags "machine-sounding phrasing."

TOKEN / COST
9. Literary ("undertow") full-chapter rewrite pass now defaults OFF for new books (existing toggle still in Book settings). This pass silently doubled prose spend per chapter.
10. Deleted 11 stale build artifacts (8 old JS bundles + 4 old CSS, ~4.6 MB dead weight in the deploy).

BUG FIXES
11. Verifier prompt had a stray duplicated comment attached to the wrong JSON field (dialogueIssues) — moved back to entryContinuous.
12. Codex name matcher now strips leading articles/possessives ("the mom," "his mom") and trailing punctuation before matching — fixes duplicate characters / wrong people in illustrations when the art director returns a role-name variant.
13. Non-streaming request timeout raised 180s → 300s (large outline/codex JSON calls on slow models were aborted mid-generation and billed with nothing kept).

DIRECT LANGUAGE (prompt de-poeticizing)
14. "ends mid-breath — your chapter is the next breath" → "the exact text the book currently ends on — continue directly from it."
15. "editor who finds the book beneath the book" → plain statement of the job.
16. "a charged, forward-leaning final image" → "an unresolved final image that pulls the reader into the next chapter."
