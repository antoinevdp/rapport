# Bloc 2 DevOps Section Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Add a one-page DevOps subsection to Bloc 2 in `main.tex` based on `antoinevdp/fizzbuzz-Efrei`, then update the Bloc 2 evidence table to replace the placeholder row.

**Architecture:** Keep `Projet Spark` as the main evidence for distributed data processing, and add a separate `Projet DevOps : fizzbuzz-Efrei` subsection to justify CI/CD, testing automation, and containerization. Restrict changes to `main.tex`, use `nous`, and verify the document with a LaTeX build.

**Tech Stack:** LaTeX, GitHub Actions, Docker, Docker Compose, Python `unittest`, `flake8`, `coverage`

---

## File Map

- Modify: `main.tex`
  - Add a new Bloc 2 subsection after the Spark content and before `\subsection{Analyse attendue}`.
  - Replace the final Bloc 2 table row placeholder with a concrete DevOps proof.
- Verify: build `main.tex` with `latexmk -pdf -interaction=nonstopmode main.tex`.

### Task 1: Insert the DevOps subsection in Bloc 2

**Files:**
- Modify: `main.tex` in Bloc 2, after the Spark subsection and before `\subsection{Analyse attendue}`

- [ ] **Step 1: Locate the insertion point in Bloc 2**

Read the end of the Spark section and confirm the insertion point is immediately before this block:

```tex
\newpage
\subsection{Analyse attendue}

Mettez en avant la conception des pipelines, le traitement distribue, les choix
de performance, l'automatisation et la maniere dont vous avez deploie ou
industrialise les traitements.
```

- [ ] **Step 2: Insert the new subsection heading and framing paragraph**

Add this block before `\subsection{Analyse attendue}`:

```tex
\subsubsection{Projet DevOps : fizzbuzz-Efrei}

En complément du projet Spark, nous mobilisons également le dépôt
\texttt{fizzbuzz-Efrei} pour justifier la dimension DevOps de ce bloc. Le périmètre
fonctionnel de l'application est volontairement simple : il s'agit d'une
implémentation Python du problème FizzBuzz accompagnée de tests unitaires. Ce choix
est justement intéressant dans le cadre du bloc 2, car il permet de concentrer la
démonstration non pas sur la complexité métier, mais sur l'industrialisation du cycle
de livraison : contrôle qualité, intégration continue, conteneurisation et préparation
au déploiement.
```

- [ ] **Step 3: Add the continuous integration explanation**

Append this paragraph after the framing block:

```tex
Le premier apport du projet concerne la chaîne d'intégration continue mise en place
avec GitHub Actions. Le dépôt contient un workflow \texttt{python-package.yml}
déclenché sur les branches \texttt{dev}, \texttt{main} et \texttt{docker}. À chaque
push, ce pipeline exécute automatiquement la même suite de vérifications sur une
matrice de versions Python \texttt{3.9}, \texttt{3.10} et \texttt{3.11}. Les étapes
enchainent l'installation des dépendances, l'analyse statique avec \texttt{flake8},
l'exécution des tests unitaires via \texttt{python -m unittest test.py}, puis la
mesure de couverture avec \texttt{coverage run} et \texttt{coverage report}. Cette
organisation montre que nous avons mis en place une validation systématique du code
avant intégration, afin de détecter rapidement les régressions, de garantir la
compatibilité sur plusieurs environnements Python et de fiabiliser les livraisons.
```

- [ ] **Step 4: Add the containerization explanation**

Append this paragraph after the CI paragraph:

```tex
Le second apport majeur du projet est la conteneurisation de l'application. Le
\texttt{Dockerfile} s'appuie sur une image \texttt{python:3.12.8-slim}, définit un
répertoire de travail dédié, installe les dépendances depuis \texttt{requirements.txt}
et exécute l'application avec un utilisateur non privilégié. Ce dernier point est
important, car il traduit une prise en compte des bonnes pratiques de sécurité dès la
phase de packaging. Le dépôt contient également un fichier \texttt{compose.yaml} qui
permet de reconstruire puis de lancer localement le service avec
\texttt{docker compose up --build}. Nous obtenons ainsi un environnement d'exécution
reproductible, indépendant de la machine du développeur, ce qui réduit fortement les
écarts entre développement, validation et livraison.
```

- [ ] **Step 5: Add the deployment and bloc-2 positioning paragraph**

Append this paragraph after the containerization paragraph:

```tex
Le projet ne montre pas un déploiement de production complet avec orchestrateur ou
infrastructure cloud, et il ne faut pas le présenter comme tel. En revanche, il montre
très clairement la mise en place des briques attendues dans une démarche CI/CD : une
application validée automatiquement, empaquetée sous forme d'image Docker et prête à
être publiée dans un registre puis déployée dans un environnement cible. Le
\texttt{README.Docker.md} documente d'ailleurs explicitement les commandes de build et
de push d'image. Dans le cadre du bloc 2, cette réalisation est pertinente car elle
démontre notre capacité à automatiser la vérification du code, à standardiser
l'exécution de l'application et à préparer une chaîne de déploiement outillée,
complémentaire des enjeux de traitement massif couverts par Spark.
```

- [ ] **Step 6: Read the inserted section in context**

Read the full Bloc 2 passage around the new subsection and confirm:

- the voice is consistently `nous`;
- the new text does not claim a production deployment that is not present in the repo;
- the length stays around one page;
- the transition from Spark to DevOps remains natural.

Expected result: the new subsection reads as a complementary project proof, not as a replacement for Spark.

### Task 2: Update the Bloc 2 evidence table

**Files:**
- Modify: `main.tex` in `\subsubsection{Preuves d'acquisition des compétences}` for Bloc 2

- [ ] **Step 1: Locate the placeholder row in the table**

Find this exact table row in Bloc 2:

```tex
Automatisation, tests, intégration et déploiement des pipelines &
  A completer (partie DevOps \& MLOps à rédiger). \\
```

- [ ] **Step 2: Replace the placeholder with the final proof text**

Replace the row with:

```tex
Automatisation, tests, intégration et déploiement des pipelines &
  Workflow GitHub Actions exécuté sur plusieurs branches et versions Python,
  combinant linting \texttt{flake8}, tests \texttt{unittest}, couverture
  \texttt{coverage}, puis conteneurisation avec Docker et exécution reproductible via
  \texttt{docker compose} pour préparer la livraison de l'application. \\
```

- [ ] **Step 3: Re-read the full table for balance and consistency**

Check that:

- the first four rows still point mainly to Spark;
- the fifth row clearly points to `fizzbuzz-Efrei`;
- the wording style matches the rest of the table.

Expected result: the table now covers all five Bloc 2 competencies with concrete evidence.

### Task 3: Verify the LaTeX document

**Files:**
- Modify: `main.tex` only if verification exposes a real integration issue

- [ ] **Step 1: Build the report**

Run:

```bash
latexmk -pdf -interaction=nonstopmode main.tex
```

Expected: `main.pdf` is produced.

- [ ] **Step 2: Inspect the build output**

Confirm that:

- there is no new LaTeX error caused by the Bloc 2 addition;
- any remaining warnings are pre-existing or unrelated missing bibliography entries already known in the document.

Expected result: the new DevOps subsection integrates without breaking the report.

- [ ] **Step 3: Clean generated verification artifacts if they should not remain in the worktree**

Run:

```bash
git restore "main.aux" "main.fdb_latexmk" "main.fls" "main.log" "main.out" "main.pdf" "main.synctex.gz" "main.toc"
```

Expected: only intended source changes remain in `git status`.

- [ ] **Step 4: Review the final diff**

Run:

```bash
git diff -- main.tex
```

Expected: the diff is limited to the new DevOps subsection and the updated Bloc 2 evidence row.
