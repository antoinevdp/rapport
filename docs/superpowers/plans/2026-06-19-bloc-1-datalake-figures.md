# Bloc 1 Datalake Figures Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Insert the three existing datalake screenshots into the Bloc 1 `Challenge Datalake` subsection as full-width figures placed immediately after their matching paragraphs.

**Architecture:** This is a focused LaTeX content edit in `main.tex`. The implementation keeps the existing report structure intact, adds three manual `figure` blocks that reference files from `assets/`, and replaces the current Swagger placeholder with the real schema screenshot.

**Tech Stack:** LaTeX, existing `main.tex` report structure, image assets under `assets/`, `latexmk` for verification

---

## File Structure

- Modify: `main.tex:555-661`
  Responsibility: add the three figure blocks in Bloc 1 and remove the Swagger placeholder box.

- Reuse: `assets/mysql-tables-datalake.png`
  Responsibility: evidence for the relational Silver/Gold storage description.

- Reuse: `assets/swagger-ui-endpoints-datalake.png`
  Responsibility: evidence for the REST endpoint organization paragraph.

- Reuse: `assets/swagger-ui-schema-datalake.png`
  Responsibility: evidence for the Swagger / OpenAPI documentation paragraph.

### Task 1: Insert the Bloc 1 datalake figures

**Files:**
- Modify: `main.tex:555-661`
- Verify: `main.tex` builds to `main.pdf`

- [ ] **Step 1: Add the MySQL structure figure after the relational storage paragraph**

Insert the following block in `main.tex` immediately after the paragraph ending with `usages concrets de consultation et d'exposition.` and before `La structure technique globale du projet peut être résumée par le schéma suivant.`

```tex
\begin{figure}[H]
    \centering
    \includegraphics[width=0.96\linewidth]{assets/mysql-tables-datalake.png}
    \caption{Capture de la structure relationnelle MySQL des couches Silver et Gold du projet Challenge Datalake.}
\end{figure}
```

- [ ] **Step 2: Add the Swagger endpoints figure after the API organization paragraph**

Insert the following block in `main.tex` immediately after the paragraph ending with `mais couvrait l'ensemble des domaines de données du projet.` and before `\paragraph{Fonctionnalités d'exposition et documentation.}`

```tex
\begin{figure}[H]
    \centering
    \includegraphics[width=0.96\linewidth]{assets/swagger-ui-endpoints-datalake.png}
    \caption{Documentation Swagger UI des endpoints de l'API du projet Challenge Datalake.}
\end{figure}
```

- [ ] **Step 3: Replace the Swagger placeholder with the schema figure**

Delete the existing placeholder block:

```tex
\begin{center}
    \fbox{\parbox{0.92\textwidth}{
        \centering
        \vspace{2.4cm}
        \textit{Emplacement réservé pour une capture de l'interface Swagger UI du projet Challenge Datalake.}
        \vspace{2.4cm}
    }}

    {\small \textit{Capture à ajouter : documentation Swagger UI de l'API Challenge Datalake.}}
\end{center}
```

Replace it with:

```tex
\begin{figure}[H]
    \centering
    \includegraphics[width=0.96\linewidth]{assets/swagger-ui-schema-datalake.png}
    \caption{Vue Swagger / OpenAPI du schéma exposé par l'API du projet Challenge Datalake.}
\end{figure}
```

- [ ] **Step 4: Build the LaTeX document and verify the figures compile**

Run:

```bash
latexmk -pdf -interaction=nonstopmode main.tex
```

Expected:

- exit code `0`;
- a line similar to `Output written on main.pdf`;
- no missing-file error for any of the three `*-datalake.png` assets.

- [ ] **Step 5: Review the final diff to confirm only the intended Bloc 1 section changed**

Run:

```bash
git diff -- main.tex
```

Expected:

- one new figure block after `\paragraph{Choix de stockage relationnel et hybride.}`;
- one new figure block after `\paragraph{Organisation de l'API REST.}`;
- the placeholder block removed and replaced by the schema figure under `\paragraph{Fonctionnalités d'exposition et documentation.}`;
- no unrelated wording changes elsewhere in `main.tex`.

- [ ] **Step 6: Commit the document change**

Run:

```bash
git add main.tex
git commit -m "add datalake figures to bloc 1"
```

Expected:

- one commit containing only the intended `main.tex` figure insertion.
