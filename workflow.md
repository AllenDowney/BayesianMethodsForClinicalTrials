# Workflow

## Environment

Before running code in this repository:

```bash
conda activate BayesianMethodsForClinicalTrials
```

Create or update the environment from the repo root (see `Makefile`):

```bash
make create_environment        # base: PyMC, ArviZ, PreliZ, SciPy stack, Jupyter, etc.
make create_environment_dev    # adds pytest, nbmake, black, flake8, jupytext, …
```

---

## Notebooks

Course notebooks live under [`notebooks/`](notebooks/). Prefer checking in executed notebooks with outputs so participants can read them on GitHub or Colab without re-running, unless binary outputs or secrets make that a bad idea.

### Running and testing

- Run notebooks from the **repository root** (or use paths relative to where data and imports live) so paths stay predictable.
- Execute a notebook locally, e.g.:

  ```bash
  cd /home/downey/BayesianMethodsForClinicalTrials && conda activate BayesianMethodsForClinicalTrials
  jupyter nbconvert --execute --inplace notebooks/example.ipynb
  ```

- After adding dev dependencies (`make create_environment_dev`), run automated notebook checks:

  ```bash
  make tests
  ```

  This runs `pytest --nbmake` on `notebooks/*.ipynb` when present.

### Optional: Markdown source with Jupytext

If you keep canonical sources as Markdown (e.g. `notebooks/some_topic.md`), convert to `.ipynb`, then execute:

```bash
cd /home/downey/BayesianMethodsForClinicalTrials && conda activate BayesianMethodsForClinicalTrials
jupytext notebooks/some_topic.md -o notebooks/some_topic.ipynb
jupyter nbconvert --execute --inplace notebooks/some_topic.ipynb
```

*(Skip the `jupytext` step if you edit `.ipynb` directly.)*

### Optional: Papermill

For parameterized runs (e.g. swapping datasets or scenarios via a `parameters` cell), use [papermill](https://papermill.readthedocs.io/) once it is installed in the environment:

```bash
papermill notebooks/lesson.ipynb notebooks/lesson_out.ipynb -p PARAM_NAME value
```

---

## Repo maintenance

| Task | Command |
|------|---------|
| Format Python | `make format` |
| Lint | `make lint` |
| Notebook tests | `make tests` |
| Clean caches | `make clean` |

Task planning for the course lives in [`project_board.md`](project_board.md).

---

## Coding conventions (notebooks)

* **Don’t hide missing data**: If a column or variable should exist, use it directly and let failures surface (e.g. `KeyError` on a missing column) instead of silent fallbacks that mask bugs.

* **Displaying DataFrames and Series**: Prefer leaving `df`, `df.head()`, `df.describe()`, etc. as the **last expression** in a cell so Jupyter renders them nicely. Use `print()` only for labels or non-display side effects; use `display()` when you need to show a frame inside branching logic.

* **Figure sizes**: Keep figures modest (e.g. on the order of 6–8 inches per side) so labels stay readable when scaled in slides or the browser.
