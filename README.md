<p align="center">
  <img src="data/androlibzoo-mark.png" alt="AndroLibZoo logo" width="200">
</p>

# AndroLibZoo

AndroLibZoo is a dataset of package names for identifying third-party library code in Android apps. It was created through software dependency analysis and is intended to support research and static analysis.

[Dataset](AndroLibZoo.lst) · [Paper](https://doi.org/10.1145/3643991.3644866) · [Research artifacts](https://doi.org/10.5281/zenodo.10072709) · [AndroSpecter](https://github.com/JordanSamhi/AndroSpecter)

## Dataset

[`AndroLibZoo.lst`](AndroLibZoo.lst) is a plain-text file with one package name per line. This version contains **34,813 entries**. Entries can represent a package or a broader namespace; for example, `com.example` can be used to match its subpackages. See the [paper](https://doi.org/10.1145/3643991.3644866) for the collection methodology.

Package-name matching is a heuristic: a match does not establish which library or version is present, and renamed or obfuscated packages may not match. Some entries are broad (for example, `io`), so matching every subpackage can also produce false positives. Choose and evaluate the matching policy for your analysis.

## Use the dataset

Download [`AndroLibZoo.lst`](AndroLibZoo.lst) or clone this repository and load the file in your analysis. The following example checks a fully qualified class name against the list, matching whole package components:

```python
from pathlib import Path

packages = set(Path("AndroLibZoo.lst").read_text(encoding="utf-8").splitlines())


def is_library_class(class_name: str) -> bool:
    package = class_name.rpartition(".")[0]
    while package:
        if package in packages:
            return True
        package = package.rpartition(".")[0]
    return False


print(is_library_class("com.google.ads.AdView"))  # True: com.google is in the list
```

Run the example from the repository root. Checking whole package components avoids treating a name such as `com.example2` as a subpackage of `com.example`.

### Use with AndroSpecter

[AndroSpecter](https://github.com/JordanSamhi/AndroSpecter) provides a `LibrariesManager` for checking Soot classes against its bundled library list:

```java
// Given a SootClass obtained from your analysis:
boolean isLibrary = LibrariesManager.v().isLibrary(sootClass);
```

See the [LibrariesManager documentation](https://github.com/JordanSamhi/AndroSpecter/wiki/LibrariesManager) for details and the [AndroSpecter repository](https://github.com/JordanSamhi/AndroSpecter) for setup. The bundled list may differ from the current file in this repository.

## Research artifacts

The [Zenodo archive](https://doi.org/10.5281/zenodo.10072709) contains the dataset and artifacts used to construct and describe it, including scripts and intermediate results.

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

Missing a library package? Please open a pull request adding it to [`AndroLibZoo.lst`](AndroLibZoo.lst). Include a link to the library or another source that helps verify the package name.

## License and contact

AndroLibZoo is available under the [MIT License](LICENSE). For questions about the study, contact [Jordan Samhi](mailto:jordan.samhi@cispa.de).
