<p align="center">
  <img src="data/androlibzoo-mark.png" alt="AndroLibZoo logo" width="200">
</p>

# AndroLibZoo

AndroLibZoo is a dataset of package names for identifying third-party library code in Android apps. It was created through software dependency analysis and is intended to support research and static analysis.

[2026 dataset](AndroLibZoo2026.lst) · [Original dataset](AndroLibZoo.lst) · [Paper](https://doi.org/10.1145/3643991.3644866) · [Research artifacts](https://doi.org/10.5281/zenodo.10072709) · [AndroSpecter](https://github.com/JordanSamhi/AndroSpecter)

## Dataset

| Version | File | Distinct nonempty entries |
| --- | --- | ---: |
| 2026 | [`AndroLibZoo2026.lst`](AndroLibZoo2026.lst) | 36,926 |
| Original | [`AndroLibZoo.lst`](AndroLibZoo.lst) | 34,813 |

The files contain one entry per line. The 2026 version contains all entries from the original list and adds 2,113 distinct entries, after trimming whitespace. The original file remains available for reproducibility. See the [paper](https://doi.org/10.1145/3643991.3644866) for the original dataset and its collection methodology.

The 2026 file contains a blank line, whitespace around some entries, and duplicates after trimming. Strip whitespace, discard empty lines, and deduplicate entries when loading it. Entries include broad namespaces as well as more specific names; some are not valid Java package identifiers.

**Choose your matching policy carefully.** In particular, the 2026 list contains `org`, so treating every entry as a package prefix would classify every `org.*` package as library code. A match does not establish which library or version is present, and renamed or obfuscated packages may not match.

## Use the dataset

Download [`AndroLibZoo2026.lst`](AndroLibZoo2026.lst) or clone this repository. The following example normalizes the entries and checks for an exact entry:

```python
from pathlib import Path

lines = Path("AndroLibZoo2026.lst").read_text(encoding="utf-8").splitlines()
entries = {entry for line in lines if (entry := line.strip())}

print("com.google" in entries)  # True
```

Run the example from the repository root. Exact membership is a starting point, not a complete library-detection policy: a class may belong to a subpackage of a listed entry. If you use prefix matching, match whole package components and evaluate the effect of broad entries on your analysis.

### Use with AndroSpecter

[AndroSpecter](https://github.com/JordanSamhi/AndroSpecter) provides a `LibrariesManager` for checking Soot classes against its bundled library list:

```java
// Given a SootClass obtained from your analysis:
boolean isLibrary = LibrariesManager.v().isLibrary(sootClass);
```

See the [LibrariesManager documentation](https://github.com/JordanSamhi/AndroSpecter/wiki/LibrariesManager) for details and the [AndroSpecter repository](https://github.com/JordanSamhi/AndroSpecter) for setup. AndroSpecter uses its own bundled list; adding the 2026 file to this repository does not update that list.

## Research artifacts

The [Zenodo archive](https://doi.org/10.5281/zenodo.10072709) contains the original dataset and artifacts used in the published study, including scripts and intermediate results. The 2026 version is available in this repository.

[![Zenodo DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.10072709.svg)](https://doi.org/10.5281/zenodo.10072709)

## Cite

If you use AndroLibZoo in your work, including through AndroSpecter, please cite:

```bibtex
@inproceedings{androlibzoo,
  title     = {AndroLibZoo: A Reliable Dataset of Libraries Based on Software Dependency Analysis},
  author    = {Samhi, Jordan and Bissyand{\'e}, Tegawend{\'e} Fran{\c{c}}ois and Klein, Jacques},
  booktitle = {2024 IEEE/ACM 21st International Conference on Mining Software Repositories (MSR)},
  year      = {2024},
  doi       = {10.1145/3643991.3644866}
}
```

## Contribute

Missing a library package? Please open a pull request adding it to [`AndroLibZoo2026.lst`](AndroLibZoo2026.lst). Include a link to the library or another source that helps verify the package name.

## License and contact

AndroLibZoo is available under the [MIT License](LICENSE). For questions about the study, contact [Jordan Samhi](mailto:jordan.samhi@cispa.de).
