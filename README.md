# kgg-django

Django app of the Knowledge Graph Generator (TPSE 2026/27, TU Darmstadt): a thin wrapper around [kgg-core](https://github.com/tpse2627-kgg/kgg-core).

How we work (shared by all repos): [process](https://github.com/tpse2627-kgg/kgg-core/blob/develop/docs/process/process.md)

## Setup and run

Requires Python 3.12+ and Git.

```
git clone https://github.com/tpse2627-kgg/kgg-django.git
cd kgg-django
python3 -m venv .venv          # Windows: python -m venv .venv
```

Activate the virtual environment (in every new terminal):

- Windows (PowerShell): `.venv\Scripts\Activate.ps1`
- Linux/macOS: `source .venv/bin/activate`

Install the dependencies (Django and kgg-core), create the database and start the server:

```
pip install -r requirements.txt
python manage.py migrate
python manage.py runserver
```

In a second terminal, check that the server is running:

```
curl localhost:8000/health     # Windows PowerShell: curl.exe localhost:8000/health
```

This should return `{"status": "ok"}`.

Run the tests with:

```
python manage.py test
```

On a server, set the environment variables `DJANGO_SECRET_KEY` (a secret random value) and `DJANGO_DEBUG=false`. Without them, development defaults are used.

## Branching

We use [git-flow](https://nvie.com/posts/a-successful-git-branching-model/) (to be confirmed by the team):

| Branch | Purpose |
|---|---|
| `main` | Released versions only (what the AG gets), each release tagged (`v0.1.0`, …) |
| `develop` | Integration branch; the default branch, all feature work is merged here |
| `feature/<issue>-<name>` | One per issue, branched from `develop`, merged back via pull request |
| `release/<version>` | Prepares a release from `develop`, merged into `main` and `develop` |
| `hotfix/<version>` | Urgent fix branched from `main`, merged into `main` and `develop` |

## Commit messages

We follow the [Karma commit convention](https://karma-runner.github.io/6.3/dev/git-commit-msg.html) / [semantic commit messages](https://gist.github.com/joshbuchea/6f47e86d2510bce28f8e7f42ae84c716) (to be confirmed by the team):

```
<type>(<scope>): <subject>

<body: what and why, wrapped at 80 characters>

<footer: Closes #12, BREAKING CHANGE: ...>
```

- **type:** `feat` (new feature), `fix` (bug fix), `docs`, `style` (formatting, no code change), `refactor`, `perf`, `test`, `build`, `ci`, `chore` (tooling, no production code)
- **scope:** optional, the part of the code, e.g. `extract`, `api`, `review-ui`
- **subject:** imperative, present tense, lowercase, no period, first line at most 70 characters
- Example: `feat(extract): add ontology-guided label extractor`
