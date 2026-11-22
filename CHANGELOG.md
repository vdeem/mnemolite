# Changelog

All notable changes to Mnemolite are documented here.

The format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/)
and the project uses [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.1.1] - 2026-11-22

Removes the Agent Skills bundle. The engine, its schema, the Python API and the
MCP tools are unchanged.

### Removed

- `skill/` Agent Skills package, `docs/skill.md` and `tests/test_skill.py`.
- Skill packaging references from `README.md`, `AGENTS.md`, `docs/status.md`
  and `MANIFEST.in`.

### Changed

- The sdist no longer contains the skill bundle; 0.1.1 ships the package,
  tests and documentation only.
- `docs/decisions.md` records the removal in ADR-019 and marks ADR-018
  superseded.

## [0.1.0] - 2026-11-18

First packaged release of Mnemolite.

### Added

- Local-first episodic memory in SQLite and ChromaDB with a semantic graph in
  SQLite.
- Zero-LLM consolidation: spaCy entity and triple extraction, lemmatized
  endpoints, negation-aware predicates, coordinated verbs, clausal complements
  and bounded sentence-scoped co-occurrence.
- Hybrid recall with a distance cutoff, configurable `RecallWeights` presets,
  typed fact projection and an agent-readable `.mnemolite/AGENT_CONTEXT.md`
  brief.
- MCP server exposing `add_memory`, `recall_memory`, `consolidate_memory`,
  `delete_memory` and `decay_memory` over stdio.
- `mnemolite` Python package, `Mnemolite` API and `mnemolite-server` console
  script.
- Agent Skills bundle at `skill/mnemolite-memory/` with workflows, memory
  policy, examples, troubleshooting, MCP configuration and a connectivity
  check.
- Packaging tests for the skill frontmatter, MCP config and a reproducibly
  built archive.

### Changed

- Rebranded the distribution, import package, CLI, environment variables,
  default database paths, brief directory, collection prefix and MCP server
  name to Mnemolite.
- Dedupe is exact-only: a correction or paraphrase is stored as a separate
  episode instead of being merged into stale text.
- Recall keeps generic query subjects such as `user` so user-centric graph
  facts remain reachable.
- Triple endpoints share entity graph keys, including enclosing NER spans and
  trailing-period normalization.
- The skill archive is generated from tracked source; it is no longer committed
  to git.

### Fixed

- Near-duplicate dedupe no longer swallows corrections.
- Deleting an episode after decay no longer removes a fact still supported by
  another episode.
- Repeated decay calls no longer compound.
- `co_occurs` edges can no longer crowd typed facts out of the graph result
  limit.
- Typed facts are returned even when the vector index is empty or every episode
  misses the distance cutoff.
- Pronoun and generic-noun subjects/objects no longer create `it`, `she`,
  `corp.`, `project` or similar junk nodes.

### Packaging

- Distribution: `mnemolite`.
- Import: `mnemolite`; console script: `mnemolite-server`.
- Python: 3.10+.
- License: MIT.
- Project and skill URLs: `https://github.com/vdeem/mnemolite`.
- Build extras: `dev` for tests, `build` for release artifacts.
- Wheel and sdist are built with `python -m build`; the wheel contains the
  server package and LICENSE, and the sdist contains the package, tests and
  project documentation.
