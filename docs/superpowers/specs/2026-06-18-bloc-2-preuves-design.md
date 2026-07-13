## Bloc 2 Preuves Table Design

### Goal

Add to Bloc 2 in `main.tex` a `\subsubsection{Preuves d'acquisition des compétences}` that mirrors the presentation style already used in Bloc 3.

### Scope

This change is limited to the Bloc 2 section.

It will:

- add a short lead-in sentence introducing the proof table;
- add a `tabularx` table with the same visual structure as Bloc 3;
- create one row per Bloc 2 competency listed at the start of the section;
- map the first four competencies to evidence already described in the `Projet Spark` subsection;
- leave the fifth competency intentionally incomplete with an explicit placeholder tied to `DevOps & MLOps`.

It will not:

- add the missing `DevOps & MLOps` narrative;
- restructure the rest of Bloc 2;
- change the Bloc 3 or Bloc 4 proof tables.

### Chosen Approach

Use the Bloc 3 proof table as the template, but tailor each Bloc 2 row to the wording and evidence already present in the Bloc 2 content.

This keeps the report visually consistent while avoiding a generic copy-paste.

### Planned Location

Insert the new proof subsection near the end of Bloc 2, after the existing synthesis/content for the Spark project and before Bloc 3 begins.

### Planned Table Content

The table will contain five rows:

1. Distributed architecture for massive data processing
   Evidence: Spark-based medallion architecture, shared `SparkSession`, distributed execution, local cluster entry point.
2. Distributed streaming system
   Evidence: CSV flight ingestion with `readStream`, append mode, checkpoints, incremental micro-batches.
3. Transform varied data for analytics at scale
   Evidence: alignment of flight and weather sources, UTC normalization, Silver cleaning, Gold analytical joins.
4. Optimize pipeline performance
   Evidence: Parquet storage, partitioning by `Year/Month/Day`, Spark SQL execution, separation Bronze/Silver/Gold.
5. Automate creation, tests, integration, deployment
   Evidence: placeholder text: `A compléter (partie DevOps & MLOps à rédiger).`

### Formatting

The subsection title, introductory sentence, `needspace`, `center`, `tabularx`, header colors, and two-column layout will follow the existing Bloc 3 pattern so the blocs read as a coherent set.

### Risks

The main risk is overstating competency 5 using evidence that is not yet written. The design avoids that by keeping the row explicitly incomplete.
