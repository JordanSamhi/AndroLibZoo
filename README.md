<p align="center">
<img width="1200px" src="https://github.com/JordanSamhi/AndroLibZoo/blob/main/data/androlibzoo_logo.png">
</p>

# AndroLibZoo

This repository hosts the AndroLibZoo dataset.

## Contributions

📢 If you find that AndroLibZoo lacks a specific package name of a library that might have been missed, please feel free to propose a pull-request, ***the better the list, the better our analyses***.

## Easier access and use

We have wrapped the AndroLibZoo dataset for easier use in your program.
The [AndroSpecter](https://github.com/JordanSamhi/AndroSpecter) library has a [LibrariesManager](https://github.com/JordanSamhi/AndroSpecter/wiki/LibrariesManager) that you can easily use:

```java
LibrariesManager manager = LibrariesManager.v();
SootClass sootClass = // Retrieve a SootClass instance
boolean isLibrary = manager.isLibrary(sootClass);

if (isLibrary) {
    System.out.println("The class is a library.");
} else {
    System.out.println("The class is not a library.");
}
```

Please checkout [here](https://github.com/JordanSamhi/AndroSpecter/wiki) for more.

If you use our dataset, even with AndroSpecter, please cite our work:

```
@inproceedings{androlibzoo,
	title        = {AndroLibZoo: A Reliable Dataset of Libraries Based on Software Dependency Analysis},
	author       = {J. Samhi and T. F. Bissyande and J. Klein},
	year         = 2024,
	month        = april,
	booktitle    = {2024 IEEE/ACM 21st International Conference on Mining Software Repositories (MSR)}
}
```

## Artifacts

All artifacts used in our study are available in Zenodo.

## Link to the Zenodo archive

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.10072709.svg)](https://doi.org/10.5281/zenodo.10072709)


:link: https://zenodo.org/record/10072709

## License

This project is licensed under the MIT LICENSE - see the [LICENSE](LICENSE) file for details

## Contact

For any question regarding this study, please contact us at:
[Jordan Samhi](mailto:jordan.samhi@cispa.de)
