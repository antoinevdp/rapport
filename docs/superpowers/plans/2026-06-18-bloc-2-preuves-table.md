# Bloc 2 Preuves Table Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Add a Bloc 2 `Preuves d'acquisition des compétences` subsection in `main.tex` that matches the Bloc 3 table style, fills the first four competency rows from the existing Spark content, and leaves the DevOps/MLOps row explicitly incomplete.

**Architecture:** This is a single-file LaTeX change in `main.tex`. Reuse the existing Bloc 3 proof-table structure so the document stays visually consistent, then verify the report still compiles cleanly with the existing LaTeX build command.

**Tech Stack:** LaTeX, `tabularx`, existing report macros/styles, local LaTeX build toolchain

---

## File Structure

- Modify: `main.tex`
  Responsibility: add the Bloc 2 proof subsection and table just before Bloc 3, following the established Bloc 3 formatting pattern.
- Verify: generated artifacts from the LaTeX build (`main.pdf`, `main.log`)
  Responsibility: confirm the document still compiles after the edit.

### Task 1: Add Bloc 2 Proof Table

**Files:**
- Modify: `main.tex` near the end of Bloc 2, after `\subsection{Analyse attendue}` and before `\section{Bloc 3 -- ...}`

- [ ] **Step 1: Locate the insertion point and copy the existing Bloc 3 pattern**

Use the Bloc 3 section as the formatting source. The new Bloc 2 subsection should use the same structure:

```tex
\subsubsection{Preuves d'acquisition des compétences}

Le tableau suivant récapitule, pour chacune des cinq sous-compétences du Bloc 2, la
réalisation concrète qui la démontre dans le projet.

\needspace{14\baselineskip}
\begin{center}
\begin{tabularx}{\linewidth}{|>{\raggedright\arraybackslash}p{4.2cm}|>{\raggedright\arraybackslash}X|}
  ...
\end{tabularx}
\end{center}
```

- [ ] **Step 2: Insert the five-row Bloc 2 table in `main.tex`**

Add the subsection and populate it with these rows:

```tex
\subsubsection{Preuves d'acquisition des compétences}

Le tableau suivant récapitule, pour chacune des cinq sous-compétences du Bloc 2, la
réalisation concrète qui la démontre dans le projet.

\needspace{14\baselineskip}
\begin{center}
\begin{tabularx}{\linewidth}{|>{\raggedright\arraybackslash}p{4.2cm}|>{\raggedright\arraybackslash}X|}
\hline
\rowcolor{tableHeader}
\thead{Compétence visée} & \thead{Réalisation et preuve dans le projet} \\
\hline
Architecture distribuée pour le traitement de données massives &
  Architecture Spark distribuée structurée en couches Bronze / Silver / Gold,
  pilotée par une \texttt{SparkSession} commune et un point d'entrée cluster
  \texttt{spark://localhost:7077}. \\
\hline
Système distribué de streaming &
  Ingestion incrémentale des vols via \texttt{readStream}, écriture en mode
  \texttt{append}, partitionnement des sorties et \textit{checkpointing} pour la
  reprise fiable des micro-batches. \\
\hline
Transformation de données variées pour l'analytique à l'échelle &
  Croisement de deux sources hétérogènes (vols CSV et météo API), normalisation
  temporelle en UTC en Silver, puis jointures analytiques en Gold avec Spark SQL. \\
\hline
Optimisation des performances des pipelines &
  Utilisation du format Parquet, partitionnement par \texttt{Year}/\texttt{Month}/\texttt{Day},
  séparation Bronze / Silver / Gold et exécution distribuée Spark SQL pour limiter
  les lectures inutiles et accélérer les agrégations. \\
\hline
Automatisation, tests, intégration et déploiement des pipelines &
  A compléter (partie DevOps \& MLOps à rédiger). \\
\hline
\end{tabularx}
\end{center}
```

- [ ] **Step 3: Check the wording against the existing Bloc 2 competency list**

Confirm that each row corresponds to one of the five competencies already listed at the top of Bloc 2 and that the fifth row remains explicitly incomplete rather than overstated.

Expected result:

```text
5 table rows present
Rows 1-4 map to written Spark content
Row 5 contains the explicit DevOps/MLOps placeholder
```

- [ ] **Step 4: Build the LaTeX document**

Run:

```bash
latexmk -pdf main.tex
```

Expected: successful PDF build with no new LaTeX errors caused by the inserted table.

- [ ] **Step 5: Inspect the diff for the intended scope**

Run:

```bash
git diff -- main.tex docs/superpowers/plans/2026-06-18-bloc-2-preuves-table.md docs/superpowers/specs/2026-06-18-bloc-2-preuves-design.md
```

Expected: only the plan file, spec file, and the Bloc 2 proof-table addition are shown.

- [ ] **Step 6: Commit**

Run:

```bash
git add main.tex docs/superpowers/specs/2026-06-18-bloc-2-preuves-design.md docs/superpowers/plans/2026-06-18-bloc-2-preuves-table.md
git commit -m "add bloc 2 competency proof table"
```

Expected: one commit containing the spec, plan, and `main.tex` change.
