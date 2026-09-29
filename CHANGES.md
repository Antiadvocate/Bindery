# Bindery patch — September 29, 2026
The deployed bundle is now index-7bd87585.js. source/bindery.readable.js is the same code unminified, for editing; the eight stale bundles and four stale stylesheets are deleted.

PROMPTS
1. Every instruction sent to a model is rewritten in plain words: the prose writer, charter, cast design, outline, proofreader, record-keeper, passage editor, voice distiller, editor's report, visual codex, illustration, portrait and cover prompts. Role-play openers ("master story architect", "forensic continuity editor") and figurative instructions ("land the image and exit", "undertow") are gone.
2. The writing rules no longer forbid naming feelings or require subtext in every line; both pushed models into jaw-clenching gesture prose. They now ask for scenes, exact nouns, dialogue that sounds like people, feelings shown mostly through action, and at most one body-part emotion per chapter.
3. The ban list covers the common machine phrases (testament, tapestry, "for a long moment", "a flicker of", "smile that didn't reach", "not X but Y", "It wasn't X. It was Y.", therapy words in the wrong mouths) and the overused AI character names.
4. Chapters are no longer all told to end on a hook image, and the recurring image is optional instead of a duty every chapter.

STORY
5. Cast & theme step before the outline: 3-8 characters with want, need, wrong belief, history, secret, how they talk, relationships and arc. The author's own characters are kept by name and filled in. The theme comes from the same call, so its names match the cast.
6. The outline is told to build cause and effect, rising pressure, set-ups that pay off, and an ending the characters earn. Threads carry a planned payoff chapter, and the writer is told not to close them early.
7. Per-character record: after every chapter the record-keeper logs where each person is, their condition, what they learned, what they want now, how they changed and any relationship change. The writer gets it before each chapter; the proofreader flags knowledge leaks and out-of-character behaviour, and those send the chapter back for revision. Shown and editable in Bible → Cast.
8. The writer sees the next three chapter summaries and the titles after that, so it can set things up without jumping ahead.
9. Overused-phrase detection: phrases the book has repeated across chapters are listed so the writer avoids them (computed locally, no tokens).
10. Line fix after every chapter, in every rigor mode: stock phrases, dash pile-ups and the book's overused phrases are found locally, and only those paragraphs go back to the prose model. This costs a fraction of a full rewrite.
11. The old literary rewrite is now the "Polish pass" (still off by default), aimed at stock phrasing and self-explaining lines instead of adding subtext.
12. Revisions and length extensions now get the story state and handoff, so they don't break continuity while fixing something else.
13. Model output is cleaned of <think> blocks, "Chapter 3: Title" headings and trailing word-count or author notes.

BUGS
14. The refusal detector threw away chapters where a character said "I can't help…" or "I'm sorry, but" near the start. Dialogue in quotes is now ignored.
15. The cast the author typed in was never sent to the outliner and was overwritten by the architect's cast.
16. Premises under 900 words skipped the charter call, so short briefs got no style guide, audience, logline or genre. The charter call always runs now; verbatim is only the fallback if it fails.
17. When a chapter's closeout failed, the previous chapter's exit state and editor note stayed in place and the next chapter picked up from the wrong scene. Both are now cleared.
18. Reader → Illustrate crashed the first time on a book with no visual codex yet.
19. Re-architect threw away written chapters without warning. It asks first now.
20. Research mode did nothing. It now turns on OpenRouter web search for the charter and outline calls.
21. The visual codex only saw the premise when the charter was verbatim (inverted condition).
22. The proofreader's JSON template had a missing comma.
23. Pausing left a chapter's stage as "drafting", so the Write screen kept showing it as live.
24. Rewrite-forward left plates, character records and thread states from the discarded chapters.
25. A line fix or pause during it could retry an aborted call; the pause signal is now shared.
26. The visual codex call ran on every outline even with illustration off; it now runs only when auto-illustrate is on (the Reader still builds it on demand).
27. Chapters not yet written can be edited in the Plan tab during a run.
28. Wrong canon facts can be deleted from the Bible.
29. Book report used the record-keeper's system prompt; it has its own now, and the pitch bans "in a world where" copy.
30. Sequels inherit where each character ended up.

TESTING
The full pipeline (charter, cast, outline, three chapters with proofing, revision, line fix and closeout, then Reader illustration) was run in headless Chromium against a mocked OpenRouter, on both the readable and minified builds, with no console errors.

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
