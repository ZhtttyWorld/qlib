```markdown
# qlib Development Patterns

> Auto-generated skill from repository analysis

## Overview

This skill teaches you the core development patterns, coding conventions, and workflows used in the `qlib` repository. `qlib` is a Python-based project (no major framework detected) for quantitative research and financial modeling. The repository emphasizes modular design, clear code style, and robust workflows for CI, features, documentation, data ingestion, and security. This guide will help you contribute effectively and maintain consistency within the codebase.

## Coding Conventions

- **File Naming:**  
  Use `snake_case` for Python files and modules.
  ```
  # Good
  data_utils.py
  model_trainer.py

  # Bad
  DataUtils.py
  modelTrainer.py
  ```

- **Import Style:**  
  Prefer **relative imports** within the package.
  ```python
  # Good
  from .utils import load_data

  # Bad
  import qlib.utils
  ```

- **Export Style:**  
  Use **named exports** (explicitly define what is public).
  ```python
  # In __init__.py
  from .core import Model, Trainer

  __all__ = ["Model", "Trainer"]
  ```

- **Commit Messages:**  
  - Freeform, sometimes prefixed with `fix`
  - Keep messages concise (average ~42 characters)

## Workflows

### Update CI Workflows and Build Metadata
**Trigger:** When releasing a new version, updating build/test infrastructure, or changing dependencies.  
**Command:** `/update-ci`

1. Edit `.github/workflows/*.yml` files to adjust CI behavior.
2. Update version metadata in `pyproject.toml`, `qlib/__init__.py`, and/or `setup.py`.
3. Optionally update `Makefile` or `CHANGELOG.md`.
4. Commit all related changes together.

**Example:**
```bash
# Update version in pyproject.toml
vim pyproject.toml

# Edit CI workflow
vim .github/workflows/ci.yml

# Commit together
git add pyproject.toml .github/workflows/ci.yml
git commit -m "chore: update CI and bump version"
```

---

### Feature or Refactor with Tests
**Trigger:** When implementing a new feature or refactoring an existing one, and ensuring correctness with tests.  
**Command:** `/feature-with-tests`

1. Edit or create implementation files (e.g., in `qlib/contrib/strategy/`, `qlib/contrib/model/`, etc.).
2. Edit or create corresponding test files under `tests/` (often with similar names).
3. Commit both implementation and tests together.

**Example:**
```python
# qlib/contrib/model/my_model.py
class MyModel:
    pass

# tests/contrib/model/test_my_model.py
def test_my_model():
    assert MyModel() is not None
```

---

### Documentation Update
**Trigger:** When documentation needs correction or improvement.  
**Command:** `/update-docs`

1. Edit one or more documentation files (`README.md`, `docs/**/*.rst`, `examples/**/*.md`, etc.).
2. Optionally update code comments or docstrings.
3. Commit documentation changes.

**Example:**
```bash
vim README.md
git add README.md
git commit -m "docs: clarify installation instructions"
```

---

### Data Collector Script Update
**Trigger:** When data collection scripts need bug fixes, API endpoint changes, or enhancements.  
**Command:** `/update-data-collector`

1. Edit one or more scripts under `scripts/data_collector/` (e.g., `utils.py`, `collector.py`).
2. Optionally update related `requirements.txt` or documentation.
3. Commit all related changes together.

**Example:**
```bash
vim scripts/data_collector/collector.py
git add scripts/data_collector/collector.py
git commit -m "fix: update API endpoint in collector"
```

---

### Security Fix: Pickle Usage
**Trigger:** When a security issue is found related to pickle usage.  
**Command:** `/fix-pickle-security`

1. Edit Python files to replace or restrict `pickle.load` usage (e.g., enforce `RestrictedUnpickler` or restrict classes).
2. Update affected modules across `qlib/` and sometimes `tests/`.
3. Commit all security-related changes together.

**Example:**
```python
# qlib/utils/pickle_safe.py
import pickle

class RestrictedUnpickler(pickle.Unpickler):
    def find_class(self, module, name):
        if module == "allowed.module" and name == "AllowedClass":
            return super().find_class(module, name)
        raise pickle.UnpicklingError("global '%s.%s' is forbidden" % (module, name))
```

## Testing Patterns

- **Framework:** Unknown (no major test framework detected)
- **Test File Pattern:**  
  - Python test files are under `tests/` and use `snake_case` naming.
  - Test files often mirror the structure and naming of implementation files.
- **Example Test File:**
  ```python
  # tests/contrib/strategy/test_my_strategy.py
  def test_my_strategy():
      result = my_strategy.run()
      assert result is not None
  ```

## Commands

| Command                 | Purpose                                                        |
|-------------------------|----------------------------------------------------------------|
| /update-ci              | Update CI workflows and build/version metadata                 |
| /feature-with-tests     | Add or refactor a feature and update/add corresponding tests   |
| /update-docs            | Update documentation files                                     |
| /update-data-collector  | Update or fix scripts in scripts/data_collector/               |
| /fix-pickle-security    | Refactor/fix code to address unsafe pickle deserialization     |
```
