# Scheme Presets

Reference folder schemes the setup wizard uses to match against intake content. Each preset is a set of numbered folders with a purpose. The wizard picks one (or blends two) based on signals in `/_intake/`.

---

## Preset: `business` (default, v1 baseline)

**For:** solo consultants, agency operators, service businesses with clients

**Signals to detect:** folders named like `clients/`, `proposals/`, `invoices/`, SOPs, retainer-shaped documents, contracts

**Scheme:**
```
00_Inbox/           Catch-all for unsorted items
01_Identity/        About, brand identity, personal positioning
02_Work/            Clients / engagements (one folder per entity)
03_Projects/        Active project work
05_Strategy/        Growth plans, financial models
06_Operations/      SOPs, processes, task board
07_Ideas/           Brainstorms, experiments
08_Publishing/      Social media, content, newsletter
09_Reference/       Read-only archive
```

---

## Preset: `researcher`

**For:** PhD students, academic researchers, lab scientists

**Signals to detect:** `.pdf` files with year-stamped names (e.g., `smith-2024.pdf`), folders like `papers/`, `experiments/`, `thesis/`, BibTeX files, citation keys

**Scheme:**
```
00_Inbox/
01_Identity/        CV, bio, research goals
02_Collaborators/   Advisor, committee, lab mates, co-authors
03_Projects/        Thesis chapters, paper drafts, grants
04_Experiments/     Lab notes, datasets, results  [new folder]
05_Papers/          Reading library, annotated PDFs  [renamed from Strategy]
06_Operations/      Writing workflow, submission SOPs
07_Ideas/           Research questions, hypotheses
08_Publishing/      Posters, talks, published work
09_Reference/       Textbooks, canonical papers (read-only)
```

---

## Preset: `student`

**For:** undergraduates, course-based learning, certification study

**Signals to detect:** folders named `courses/`, `lectures/`, `assignments/`, textbook PDFs, syllabus docs, weekly-numbered files

**Scheme:**
```
00_Inbox/
01_Identity/        About you, goals, study plan
02_Courses/         One folder per course  [renamed from Work]
03_Projects/        Assignments, term papers, capstones
04_Study-Notes/     Concept notes, flashcards, summaries  [new folder]
05_Resources/       Textbooks, cheat sheets  [renamed from Strategy]
06_Operations/      Study routines, exam prep SOPs
07_Ideas/           Career ideas, side projects
09_Reference/       Course readings archive
```

---

## Preset: `personal`

**For:** personal knowledge base, journaling, reading tracker, life planning

**Signals to detect:** journal entries, reading lists, personal projects, blog drafts, no client/course/paper folders

**Scheme:**
```
00_Inbox/
01_Identity/        About, goals, values
02_People/          Relationships, contacts  [renamed from Work]
03_Projects/        Personal projects, goals in motion
05_Journal/         Reflections, reviews  [renamed from Strategy]
06_Operations/      Routines, habits, SOPs
07_Ideas/           Thoughts, hunches
08_Reading/         Books, articles, notes  [renamed from Publishing]
09_Reference/       Saved content archive
```

---

## Default (fallback, generic)

Used when intake is empty, when no preset matches clearly, or when user rejects the proposed preset.

**Scheme:**
```
00_Inbox/
01_Identity/
02_Work/
03_Projects/
05_Strategy/
06_Operations/
07_Ideas/
08_Publishing/
09_Reference/
```

---

## Blending presets

If intake matches two presets (e.g., a PhD student who also freelances), blend them:
- Keep folders shared by both
- Add distinctive folders from both (up to ~10 numbered folders total)
- Present as a custom scheme — tell user which presets it drew from

Example blend (researcher + business):
```
00_Inbox/
01_Identity/
02_Clients/         (from business)
03_Projects/
04_Experiments/     (from researcher)
05_Papers/          (from researcher)
06_Operations/
07_Ideas/
09_Reference/
```

---

## Creating a new preset

If you're adapting this template for a use case not covered above, add your preset here and submit a PR. Each preset needs:

1. Name + one-line description
2. Target user
3. Signals to detect in intake
4. Folder scheme (use the 00-09 numbering pattern)
5. Rationale for any custom folders

Keep numbers 04 consistently available for a distinctive new folder — that's the customization slot.
