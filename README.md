# AndroLibZoo

This repository hosts the AndroLibZoo dataset and the artifacts used in our study on Android libraries.

:warning: :warning: :warning:
:loudspeaker: All artifacts are available in Zenodo, **<ins>LINK BELOW</ins>**.

## Link to the Zenodo archive

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.10072709.svg)](https://doi.org/10.5281/zenodo.10072709)


:link: https://zenodo.org/record/10072709

## Artifacts

The `artifacts` folder contains all the artifacts, i.e., datasets, scripts, results, source code, etc., to reproduce our study and produce AndroLibZoo.

* The file `AndroLibZoo.lst` is our dataset.
* The subfolders in artifacts are as follows:
  * The `motivation` folder contains all artifacts related to our motivation study (i.e., Section 2).
  * The `methodology` folder contains all artifacts related to our methodology (i.e., Section 3). In particular, we present:
    * How we gather libraries from Maven
    * How we gather libraries from Google
    * How we gather transitive dependencies
    * How we gather libraries from open source apps
    * How we gather libraries from Gradle plugin libraries
    * How we refined our list of libraries.
  * The `description` folder contains the artifacts useful to describe our dataset (i.e., Section 4).

All folders contain scripts that start with "XX_", with XX being a number that represents the order in which scripts need to be executed. Some of the scripts need to be parametrized with names of servers, AndroZoo API keys, prefixes for Redis server, etc.


## License

This project is licensed under the MIT LICENSE - see the [LICENSE](LICENSE) file for details

## Contact

For any question regarding this study, please contact us at:
[Jordan Samhi](mailto:jordan.samhi@cispa.de)
