# Bindery patch — September 29, 2026 (4): the writer writes the book
The bundle is now index-4cf3f3c4.js.

A good model asked directly for a story writes one that holds together. Bindery was making it write worse:
- The plot came from the "architect" model (DeepSeek by default), and its events were handed to the prose model as things that "must all happen, checked one by one". A missing one sent the chapter back for a full rewrite. The prose model was writing someone else's outline under orders.
- The prose model never saw the book. It got a 100-word summary per earlier chapter, the last few lines, and a stack of notes.
- It was buried in instructions: 13 craft rules, ban lists, theme notes, "what the chapter is about underneath", motifs. Writing by checklist reads like it.

What changed:
1. Planning (charter, characters, outline) uses the prose model unless you pick a separate architect. Books still on the old DeepSeek architect default are switched to "same as the prose model" when the app loads.
2. The writer gets the book so far as text: every written chapter in full, up to about 60,000 tokens. Beyond that, the oldest chapters are sent as summaries, with the established facts and where the characters stand. The newest chapters are always in full.
3. The writer's instructions are the style, the author's requirements and brief, the main characters and one sentence on how to write: 250 tokens instead of 1,650. The craft rules, ban lists, theme, motifs, "turn" and "subtext" are gone from the writer. So are the rules on jokes and powers added earlier today.
4. The chapter plan is presented as a guide written before the book started: "where the story so far has gone differently, follow the story and keep it making sense." The outline asks for what happens, not turns, subtext and motifs.
5. The character notes step asks for characters as the author would note them. Characters from an existing film, book or game are described as they are there. The lie/need/wound template is gone.
6. Proofing (Standard) sends a chapter back only for continuity errors or things that make no sense. It reads the end of the previous chapter itself. Missing planned events are only enforced in Maximum.
7. Cost: the manuscript is sent first in the message, one block per chapter, so it is read from cache. On Claude models each chapter block carries a cache marker, and chapter N reuses what chapter N-1 cached. DeepSeek, Gemini and the rest cache the prefix automatically. Late chapters send more input than before; most of it is billed at cache rates (0.1x on Claude and DeepSeek).
8. Stock-phrase detection, the paragraph line fix and repeated-phrase detection stay. They run locally and cost the writer nothing.

# Bindery patch — September 29, 2026 (3b): chapters cut off mid-word
1. Chapters that hit the model's output limit were accepted as finished ("You will come", "the mo"). The app now reads why the model stopped. A chapter that stopped on the limit, or ends mid-sentence, is continued from its last word (up to two continuations).
2. The output allowance per chapter is 3 tokens per target word plus 2,500 (was 2 plus 600). Thinking models spend this allowance before the prose, and you only pay for what is produced.
3. Five-word phrases repeated across chapters count as repeated phrases.

