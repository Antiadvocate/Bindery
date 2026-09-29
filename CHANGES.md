# Bindery patch — September 29, 2026 (3): cheaper runs
The bundle is now index-17e4ee1e.js.

1. Thinking off by default. Many current models reason before they answer and bill that as output tokens, the expensive side. Every call now sends OpenRouter's reasoning switch set to off. A model that rejects the switch (400) is asked again without it, once, and remembered for the session. Sliders sheet → Model thinking: Off, A little, or the model's default.
2. One session id per book on every call. OpenRouter picks a provider per conversation by hashing the first system message and the first user message; Bindery's user message changes on every call, so calls could hop between providers and miss the cache for the system prompt (1.5-4k tokens of rules, brief and cast, sent with every chapter call). With a session id, OpenRouter keeps the book on one provider and the prefix is read from cache: 0.1x the input price on DeepSeek, 0.25x on Gemini, Grok and Moonshot.
3. Style notes from proofing (lines that state the meaning, lines that miss the style guide) no longer trigger a full chapter rewrite. Those sentences go to the paragraph line fix. Full rewrites happen only for a missing event, a broken opening, a continuity error, a character acting wrong, a wrong ending or a chapter where nothing changes.
4. New books allow one full rewrite per chapter instead of two. Sliders sheet → Full rewrites per chapter: None, One, Two.
5. Spending limit per book, in dollars and cents. The press pauses with a message when the book reaches it; raise it and Resume.
6. In long books the writer gets at most 70 established facts per chapter: the first 20, the last 25, and any that mention someone or somewhere in that chapter. The proofreader gets 60 the same way.
7. A JSON reply that can't be parsed is retried once instead of twice.
8. New books default to deepseek/deepseek-v3.2 for prose, editing and planning (about $0.21 in / $0.31 out per million tokens, cache reads $0.02, per OpenRouter's listing). The pickers show live prices if you want something else.
9. Pulse → Spend shows how many input tokens were read from cache.

