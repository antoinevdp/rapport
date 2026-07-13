# Bloc 1 Datalake Figures Design

## Goal

Add the three existing datalake screenshots from `assets/` into the `Challenge Datalake` subsection of Bloc 1 in `main.tex`.

The figures should be inserted as full-width standalone figures placed immediately after the paragraph they support.

## Scope

This change is limited to the Bloc 1 `Challenge Datalake` narrative.

It will:

- insert three real image-based figures using the existing files in `assets/`;
- place each figure directly after the most relevant paragraph;
- replace the current Swagger placeholder box with a real figure;
- add concise captions aligned with the surrounding academic tone.

It will not:

- restructure Bloc 1;
- change the wording of unrelated paragraphs;
- move the images to another directory unless required by the existing LaTeX include pattern.

## Available Assets

- `assets/mysql-tables-datalake.png`
- `assets/swagger-ui-endpoints-datalake.png`
- `assets/swagger-ui-schema-datalake.png`

The file names are descriptive enough to map them to the report content.

## Chosen Approach

Use three independent full-width `figure` blocks placed inline in the reading flow.

This is preferable to grouping the images at the end of the subsection because each screenshot then acts as direct evidence for the paragraph that introduces it.

## Planned Placement

### 1. MySQL tables screenshot

Insert `mysql-tables-datalake.png` immediately after `\paragraph{Choix de stockage relationnel et hybride.}`

Reasoning:

- this paragraph explains the structured Silver and Gold storage in MySQL;
- the screenshot likely shows the relational tables that support that explanation;
- it strengthens the proof of relational modeling inside Bloc 1.

### 2. Swagger UI endpoints screenshot

Insert `swagger-ui-endpoints-datalake.png` immediately after `\paragraph{Organisation de l'API REST.}`

Reasoning:

- this paragraph lists the API route families;
- the screenshot likely shows the browsable endpoint catalog;
- it provides a visual proof that the data exposure layer is organized and consumable.

### 3. Swagger UI schema screenshot

Insert `swagger-ui-schema-datalake.png` immediately after `\paragraph{Fonctionnalités d'exposition et documentation.}`

Reasoning:

- this paragraph explicitly discusses Swagger, OpenAPI, and `drf-spectacular`;
- the screenshot likely shows the generated schema/documentation view;
- it is a better fit here than under the generic API organization paragraph.

## Placeholder Replacement

The current placeholder block under `\paragraph{Fonctionnalités d'exposition et documentation.}` should be removed entirely and replaced by the real schema screenshot figure.

This avoids duplicate evidence and keeps the section clean.

## Formatting

- Use standard LaTeX `figure` blocks consistent with the rest of the report.
- Keep the images full width relative to the text block, while preserving margins and readability.
- Use short captions describing what the screenshot demonstrates rather than repeating the paragraph verbatim.
- Preserve the report's existing figure numbering behavior.

## Draft Captions

1. `Capture de la structure relationnelle MySQL des couches Silver et Gold du projet Challenge Datalake.`
2. `Documentation Swagger UI des endpoints de l'API du projet Challenge Datalake.`
3. `Vue Swagger / OpenAPI du schéma exposé par l'API du projet Challenge Datalake.`

## Risks

The main risk is oversizing the screenshots and hurting page flow.

The implementation should therefore choose widths that keep the images readable without overwhelming the surrounding text.
