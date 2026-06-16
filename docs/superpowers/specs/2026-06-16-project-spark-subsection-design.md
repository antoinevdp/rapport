# Project Spark Subsection Design

## Scope

Expand only the `Projet Spark` subsection in `main.tex`, with a specific focus on the three existing Medallion paragraphs:

- `Couche Bronze : ingestion batch et streaming`
- `Couche Silver : nettoyage, normalisation et mise en coherence`
- `Couche Gold : jointures analytiques et restitution`

The existing code blocks must remain unchanged.

## Goal

Make the `Projet Spark` explanation more detailed and more technical without changing the structure of the subsection or rewriting it into a different format.

The revised text should better explain:

- how the Bronze layer ingests and persists raw data,
- how the Silver layer prepares data for reliable joins,
- how the Gold layer produces analytical outputs from normalized data.

## Recommended Approach

Keep the current subsection structure and enrich the three Medallion-layer paragraphs in place.

This is the smallest correct change because it:

- preserves the current flow of the report,
- adds technical depth exactly where the user asked for it,
- avoids touching the existing code listings,
- avoids introducing new sub-subsections or diagrams.

## Content Changes

### Bronze

Expand the explanation of the ingestion layer with:

- the distinction between batch weather ingestion and streaming flight ingestion,
- why Parquet is used as the raw persistence format,
- the role of partitioning by date in downstream reads,
- the role of checkpointing for recovery and fault tolerance,
- the benefit of storing raw but already structured data for replay and debugging.

### Silver

Expand the explanation of the transformation layer with:

- filtering of the useful flight perimeter,
- schema cleanup and removal of irrelevant columns,
- parsing and normalization of timestamps,
- timezone conversion to UTC for both departure and arrival events,
- weather cleanup to support time-aligned joins,
- writing curated datasets into the Silver warehouse.

### Gold

Expand the explanation of the analytical layer with:

- the use of Spark SQL for analytical joins,
- the join keys used to align flight and weather data,
- the move from operational tables to consumption-oriented outputs,
- the production of aggregated indicators,
- the export to MariaDB through JDBC as a serving layer.

## Tone And Constraints

- Keep the tone mostly technical.
- Keep the text in report prose, not bullet-heavy implementation notes.
- Do not modify code blocks.
- Do not change the surrounding structure unless needed for coherence.

## Expected Result

After the edit, the `Projet Spark` subsection should read as a clearer technical explanation of the data pipeline, especially the responsibilities and mechanics of Bronze, Silver, and Gold.
