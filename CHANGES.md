# Bindery patch — September 29, 2026 (2)
The bundle is now index-bf72c645.js.

1. Model pickers: only the first picker opened ever showed the model list; every other one stayed on "Loading the OpenRouter directory…". The list was cached after the first load, and the other pickers saw the cache, skipped the fetch, and never read it. Every picker now reads the cached list.
2. Chapters and Words / chapter are plain numeric text fields now. The old number inputs rewrote the value on every keystroke, which fights the phone keyboard. You can type any value; it is checked when you leave the field (1-200 chapters, 100-12,000 words).
3. Words per chapter can be changed after planning and during a run, in the sliders sheet. It applies to chapters not yet written.

