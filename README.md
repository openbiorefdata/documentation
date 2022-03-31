The Open Bio Ref Dataset provides genomic reference data and software packages
for use with [Galaxy](https://galaxyproject.org/) and
[Bioconductor](https://bioconductor.org/) applications. The reference data is
available for hundreds of reference genomes and has been formatted for use with
a variety of tools. The available configuration files make this data easily
incorporable with a local Galaxy server without additional data preparation.
Additionally, data experiments for _R / Bioconducutor_ are provided as packages
that can be downloaded and installed into an _R_ environment.

## Data organization

Broadly, the data is organized as versioned objects for reference data, and data
packages for use with the _R_ programming language. The reference data is
primarily intended for use with the Galaxy application, and has been formatted
for easy configuration. In the future, additional formats may be provided. The
packages are intended for use with _R / Bioconductor_.

### Reference data

The reference data is comprised mainly of genome sequence builds and associated
prebuilt indexes for a variety of tools available for the Galaxy platform. In
addition, Galaxy-specific configuration files are available that make the data
discoverable by Galaxy tools. For the time being, the reference data is
available only by mounting the data via a
[CernVM-FS](https://cernvm.cern.ch/fs/) (CVMFS) client and configuring Galaxy to
use the mount as its reference data path.

Examples of types of data included:
* twoBit (.2bit) and FASTA (.fa) sequence files
* Bowtie 2 and BWA indexes
* Mutation Annotation Format (.maf) files
* SAMTools FASTA indexes (.fai)

The following folder structure is available once the data is mounted via CVMFS.
There are two primary directories in the data repository:

* _/managed_: Data generated with [Galaxy Data
  Managers](https://galaxyproject.org/admin/tools/data-managers/), organized by
  data table (index format), then by genome build.
* _/byhand_: Data generated prior to the existence/use of Data Managers,
  manually curated.

These directories have somewhat different structures:

* _/managed_ is organized by index type, then by genome build (Galaxy dbkey)
* _/byhand_ is organized by genome build, then by index type

Both directories contain a location subdirectory, and each of these contain a
_tool_data_table_conf.xml file_:

* _/managed/location/tool_data_table_conf.xml_
* _/byhand/location/tool_data_table_conf.xml_

Galaxy consumes these _tool_data_table_conf.xml_ files and the _.loc_ "location"
files they reference. The paths contained in these files are valid once the data
from this repository is mounted via CVMFS.

### Data experiment packages

Data experiment packages are large-scale resources representing experimental
results that serve as pedagogical aids, benchmarks, or reference resources to
enable _R _users to conduct genomic studies. Example data sets range from bulk
RNAseq to recent single-cell genomic analyses, with many other data types
represented. Data packages will be available via the http or s3 protocols.

Data packages are arranged as objects presented in a standardized naming scheme
that follows a pattern known as a 'CRAN-style' repository. This organization
facilitates direct use of the data packages in _R_, without additional software
requirements. The basic format is

* _/packages/&lt;version>/data/experiment/&lt;OS-specific path>/PACKAGES_
  containing an index of available packages for a particular version and
  operating system.
* _/packages/&lt;version>/data/experiment/&lt;OS-specific
  path>/&lt;package_name> _providing the actual data package.
* The _data/experiment_ component may be replaced with _data/annotation_ and
  _bioc_, depending on the nature of the data package – _data/experiment_
  packages provide existing experiments; _data/annotation_ provide resources
  analogous to the _Galaxy_-oriented reference data; _bioc_ provide software
  packages allowing computation on experiment or annotation data.

The _&lt;version>_  reflects the (semi-annual) _Bioconductor_ release in use,
e.g., the current release as of 1 March 2022 is 3.14; a new release 3.15 is
anticipated in May 2022. The _&lt;OS-specific path>_ supports packages for use
under Windows, macOS, and Linux environments; cloud-based deployments will use
Linux packages. The _&lt;package_name>_ includes the package version within the
release, as well as information about compression and other details relevant to
use.

The CRAN-style repository reflected in the data experiment resources makes it
straight-forward for users to discover and use available resources using
standard _R / Bioconductor_ commands by simply setting the 'BioCmirror' _R
_option to point to the path of the versioned resource, e.g., for the current
release _https://&lt;S3-bucket>/packages/3.14_.

_R / Bioconductor _packages in the current release branch may have 'bug fixes'
applied, and in the current development branch may undergo frequent changes as
new features are added. The _R / Bioconductor _build system updates packages on
a regularly scheduled basis, and it is essential that the AWS resources remain
synchronized with the latest _R / Bioconductor _build system products. As such,
in addition to periodic release, package updates will also be periodically
pushed to the AWS Open Data bucket whenever needed.
