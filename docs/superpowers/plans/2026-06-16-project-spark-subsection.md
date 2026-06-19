# Project Spark Subsection Expansion Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Expand the `Projet Spark` subsection in `main.tex` with more technical detail for the Bronze, Silver, and Gold layers while keeping the existing code blocks unchanged.

**Architecture:** The change stays entirely inside the existing `Projet Spark` subsection of `main.tex`. The implementation enriches three existing explanatory paragraphs in place so the report remains structurally identical while becoming more explicit about ingestion, normalization, analytical joins, and persistence choices.

**Tech Stack:** LaTeX, plain text editing, existing report structure, optional `pdflatex` verification

---

## File Structure

- Modify: `main.tex`
  - Contains the `Projet Spark` subsection.
  - The target text is the prose around the existing Bronze, Silver, and Gold paragraphs.
  - The existing Python code listings in those three parts must remain byte-for-byte unchanged.

- Reference: `docs/superpowers/specs/2026-06-16-project-spark-subsection-design.md`
  - Approved design for the content expansion.

- Create: `docs/superpowers/plans/2026-06-16-project-spark-subsection.md`
  - This implementation plan.

### Task 1: Expand Bronze Layer Explanation

**Files:**
- Modify: `main.tex:640-666`
- Reference: `docs/superpowers/specs/2026-06-16-project-spark-subsection-design.md`

- [ ] **Step 1: Confirm the current Bronze paragraph boundaries**

Read the block beginning at `\paragraph{Couche Bronze : ingestion batch et streaming.}` and ending immediately before the Bronze code listing.

Expected text focus:

```tex
\paragraph{Couche Bronze : ingestion batch et streaming.}
La couche \textit{Bronze} centralise la donnée brute.
```

- [ ] **Step 2: Rewrite only the Bronze prose before the code block**

Replace the current Bronze explanatory paragraph with expanded prose that explicitly covers batch weather ingestion, streaming CSV ingestion for flights, Parquet persistence, date partitioning, checkpointing, and replay/debug value.

Use this replacement text:

```tex
\paragraph{Couche Bronze : ingestion batch et streaming.}
La couche \textit{Bronze} centralise la donnée brute et correspond au point d'entrée
technique du pipeline distribué. Elle reçoit des flux de natures différentes sans
chercher à les harmoniser immédiatement, ce qui permet de conserver une trace fidèle
des données réellement collectées. Dans notre projet, cette couche est alimentée par
deux mécanismes distincts. Le premier est un traitement batch, porté par
\texttt{ingest.py}, qui interroge l'API Open-Meteo pour récupérer des historiques
météo sur plusieurs localisations puis construit un DataFrame Spark avant de
persister les résultats en Parquet. Le second est un traitement streaming, porté par
\texttt{streaming.py}, qui lit les données de vols depuis des fichiers CSV déposés
dans un répertoire source et les intègre progressivement via \texttt{readStream}.

Ce choix technique est important, car il montre que la couche Bronze n'est pas
seulement un espace de dépôt passif. Elle constitue une zone d'atterrissage capable
d'absorber à la fois des extractions historiques et un flux incrémental. Le format
Parquet a été retenu pour cette couche brute car il reste compact, colonne par
colonne, tout en étant immédiatement exploitable par Spark pour des lectures
sélectives. Le partitionnement des vols par \texttt{Year}, \texttt{Month} et
\texttt{Day} améliore également les performances des traitements aval, puisqu'il
permet de limiter les scans à une période donnée au lieu de relire l'ensemble du
jeu de données.

La Bronze matérialise aussi les premières garanties de robustesse du pipeline. Dans
le cas du streaming, le \textit{checkpointing} conserve l'état du flux et l'avancement
des micro-batches, ce qui permet une reprise plus fiable après interruption sans
retraiter arbitrairement tous les fichiers déjà vus. Cette approche est essentielle
dans un contexte Big Data, car elle sépare clairement la collecte de la logique
d'analyse. En cas d'erreur dans les transformations futures, nous pouvons rejouer les
traitements Silver et Gold à partir d'une donnée brute déjà stockée, sans devoir
réinterroger l'API météo ni reconstruire manuellement les entrées de vols.
```

- [ ] **Step 3: Verify the Bronze code block is unchanged**

Check that the listing starting with the following line is identical before and after the edit:

```tex
flights = spark.readStream.format("csv").schema(schema) \
```

Expected: only surrounding prose changed; the `lstlisting` block is untouched.

### Task 2: Expand Silver Layer Explanation

**Files:**
- Modify: `main.tex:673-698`
- Reference: `docs/superpowers/specs/2026-06-16-project-spark-subsection-design.md`

- [ ] **Step 1: Confirm the current Silver paragraph boundaries**

Read the block beginning at `\paragraph{Couche Silver : nettoyage, normalisation et mise en coherence.}` and ending immediately before the Silver code listing.

Expected text focus:

```tex
\paragraph{Couche Silver : nettoyage, normalisation et mise en coherence.}
La couche \textit{Silver} est portée principalement par \texttt{cleaning.py}.
```

- [ ] **Step 2: Rewrite only the Silver prose around the current code block**

Replace the current Silver explanatory prose with expanded text that explains perimeter filtering, schema cleanup, timestamp parsing, UTC normalization, weather cleanup, and persistence to the Silver warehouse.

Use this replacement text:

```tex
\paragraph{Couche Silver : nettoyage, normalisation et mise en coherence.}
La couche \textit{Silver} est portée principalement par \texttt{cleaning.py}. C'est
à ce niveau que la donnée brute devient techniquement exploitable pour des jointures
et des calculs analytiques. Le rôle de cette couche n'est plus de simplement stocker
les entrées telles qu'elles arrivent, mais d'appliquer un cadre de qualité commun
aux deux flux. Pour les vols, cela commence par un recentrage du périmètre sur les
aéroports et les colonnes réellement utiles à l'étude. Cette réduction du bruit est
importante dans Spark, car elle diminue le volume de données manipulées dans les
étapes suivantes et évite de transporter des attributs sans valeur pour l'analyse.

Le travail principal de cette couche porte ensuite sur la normalisation temporelle.
Les heures de départ et d'arrivée sont d'abord converties en \texttt{timestamp}, puis
recalculées dans un référentiel commun en UTC à partir des fuseaux horaires des
aéroports d'origine et de destination. Cette étape est décisive : sans elle, un vol
et une observation météo pourraient être rapprochés alors qu'ils ne correspondent
pas au même instant réel. Le projet résout donc une difficulté classique des données
massives hétérogènes : rendre comparables des événements issus de systèmes qui n'ont
pas la même représentation du temps.

La partie météo suit la même logique de fiabilisation. Les colonnes entièrement
nulles sont supprimées, les dates sont homogénéisées et les observations sont
préparées pour une granularité horaire cohérente avec les heures de départ des vols.
Une fois ces traitements effectués, les jeux de données sont enregistrés dans le
warehouse Silver sous forme de tables Spark. Cette persistance intermédiaire est
utile techniquement, car elle isole une version nettoyée et réutilisable de la
donnée : les étapes Gold peuvent alors se concentrer sur les jointures et les
agrégations sans avoir à répéter les opérations de préparation.
```

- [ ] **Step 3: Verify the Silver code block is unchanged**

Check that the listing containing the following lines is identical before and after the edit:

```tex
df = df.withColumn("OriginTimezone", mapping_expr[col("Origin")])
df = df.withColumn("DestTimezone", mapping_expr[col("Dest")])
```

Expected: only the descriptive prose changed; the Python listing remains untouched.

### Task 3: Expand Gold Layer Explanation

**Files:**
- Modify: `main.tex:699-724`
- Reference: `docs/superpowers/specs/2026-06-16-project-spark-subsection-design.md`

- [ ] **Step 1: Confirm the current Gold paragraph boundaries**

Read the block beginning at `\paragraph{Couche Gold : jointures analytiques et restitution.}` and ending after the explanatory paragraph following the Gold code listing.

Expected text focus:

```tex
\paragraph{Couche Gold : jointures analytiques et restitution.}
La couche \textit{Gold} s'appuie sur un script Spark SQL dédié.
```

- [ ] **Step 2: Rewrite only the Gold prose around the current code block**

Replace the current Gold explanatory prose with expanded text that explains Spark SQL joins, join keys, analytical outputs, and JDBC export to MariaDB.

Use this replacement text:

```tex
\paragraph{Couche Gold : jointures analytiques et restitution.}
La couche \textit{Gold} s'appuie sur un script Spark SQL dédié. Elle correspond au
moment où l'on quitte une logique de préparation technique pour entrer dans une
logique de restitution analytique. Les tables Silver de vols et de météo y sont
croisées à l'aide de requêtes Spark SQL construites pour rapprocher deux dimensions
majeures du projet : la localisation et le temps. Concrètement, la jointure repose
sur l'aéroport d'origine du vol et sur une clé horaire dérivée de l'heure de départ,
ce qui permet d'associer à chaque vol les conditions météo les plus pertinentes au
moment où il est censé décoller.

Ce choix de modélisation est central pour la qualité des résultats. Une jointure
approximative sur la seule date ou sur une zone géographique trop large aurait
produit des indicateurs peu fiables. En imposant une granularité horaire et une
correspondance par localisation, le pipeline transforme deux flux indépendants en un
jeu d'analyse cohérent. La couche Gold peut alors produire des objets directement
consommables : retard moyen par compagnie, impact de la neige ou des précipitations,
vols les plus affectés par certaines conditions météo, ou encore ratios de retards
par transporteur.

Sur le plan technique, Spark SQL apporte ici deux avantages. D'une part, il permet
d'exprimer clairement les jointures et les agrégations dans une forme déclarative,
plus lisible pour un traitement analytique complexe. D'autre part, il bénéficie de
l'exécution distribuée de Spark pour calculer ces indicateurs sur des volumes plus
importants qu'un traitement local classique. Les résultats finaux sont ensuite
exportés vers MariaDB via JDBC. Cette sortie relationnelle joue le rôle de couche de
service : elle facilite la consultation des tables Gold par d'autres outils,
éventuellement un dashboard, un outil BI ou un composant applicatif, sans imposer à
chaque consommateur de relancer la logique Spark complète.
```

- [ ] **Step 3: Verify the Gold code block is unchanged**

Check that the listing starting with the following lines is identical before and after the edit:

```tex
query = """
    SELECT f.Airline, f.Origin, f.Dest, f.ArrDelayMinutes,
```

Expected: the SQL example remains unchanged; only the surrounding narrative becomes more detailed.

### Task 4: Validate The Edited Report

**Files:**
- Modify: `main.tex`

- [ ] **Step 1: Review the final diff in the Spark subsection**

Check that changes are limited to the `Projet Spark` subsection and specifically to the explanatory prose around Bronze, Silver, and Gold.

Expected: no edits in Bloc 1, no edits in other sections, no code-block changes.

- [ ] **Step 2: Compile the LaTeX document**

Run:

```bash
pdflatex -interaction=nonstopmode main.tex
```

Expected: PDF build completes and updates `main.pdf` without LaTeX syntax errors caused by the rewritten prose.

- [ ] **Step 3: Spot-check the generated PDF text flow**

Open the generated PDF in the existing LaTeX workflow and confirm that:

```text
- the Bronze paragraph wraps correctly,
- the Silver paragraph wraps correctly,
- the Gold paragraph wraps correctly,
- code blocks remain in place,
- figures and surrounding section breaks still look coherent.
```

- [ ] **Step 4: Record completion state**

Expected final state:

```text
main.tex contains a more technical Project Spark subsection,
existing code listings are unchanged,
the document still compiles successfully.
```
