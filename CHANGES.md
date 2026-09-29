# Bindery patch — September 29, 2026 (7): leaks, cut-offs, names, line fix
The bundle is now index-778c9ad9.js.
1. The model's own notes leaked into the book. Asked to continue a cut-off chapter, the model wrote its plan inside <reasoning> tags, and only <think> was stripped. Every reply is now cleaned of <think>, <thinking>, <reasoning>, <analysis>, <scratchpad> and similar blocks, including one left unclosed.
2. Chapters could still end mid-word ("The rab"). A continuation that came back as nothing but notes ended the loop and the cut-off text was kept. That reply now counts as one try and the loop goes on (up to three continuations). A chapter still cut off after the last one ends on its last whole sentence.
3. Names the reader was never given. The writer holds every character's notes under their real names, so it wrote "Korn" for the man the book had only called "Sparky", and "Thrace" before anyone named the captain. The record now keeps what each person has been called on the page. The writer and the editor are told who the reader hasn't met yet, and the editor counts a name the reader was never given as a continuity error.
4. The line fix rewrote flagged paragraphs without seeing their neighbours, which made replies that answer nothing ("Neither do I") and lines that repeat the next paragraph. It now sees the paragraph before and after each one, unchanged.
# Bindery patch — September 29, 2026 (6): any being that is aware
The bundle is now index-dee44fc9.js.

1. The ground text is now "How anything that is aware works". It covers people, animals, swarms, gods, ghosts and machines that know themselves. Each kind of being grips through what it has, and lives in the world its senses and needs make, at its own scale of time. It is written from inside that world, never as a human in a costume. Things that aren't aware don't grip; they are how the world appears to the beings that do.
2. Character notes gain "what it is and how it perceives": its senses, what its world is made of, its scale of time. "How they talk" is now "how it talks or communicates" (voice, body, sound, signal).
3. The editor also flags a non-human written as a human in a costume.

