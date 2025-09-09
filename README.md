# clustertool

A simple command line tool for working with Kubernetes clusters.

## Installation

### Prerequisites

* __Z Shell__ - may work with Bash but not tested.
* __crudini__ - there is a system package for most Linux distros.  Mac users will probably want to install to a Python virtual environment - mess with the system Python at your own risk.

### The Installer

Run ```install.sh``` from this repository.  The executable will be installed to ```$HOME/bin/cluster``` and sample configuration will be created in ```$HOME/etc/cluster.conf```.  It is up to you to decide whether to include ```$HOME/bin``` in your path.

## In Use

The tool is currently based largely around the naming convention for EKS clusters in my place of work so the idiosyncrasies found therein are derived from that.  I am attempting to make it a little more general while retaining its simplicity.

### Configuration

Configuration is currently only used for easy identification and manipulation of EKS clusters.  The configuration file uses the .ini format and contains three stanzas:

* ```[accounts]``` contains entries that correlate one or more arbitrary account names to an AWS account number.  The format of eatch entry is ```123456123456 = dev np``` where "123456123456" is the AWS account number and "dev np" are the shorthand account names associated with that AWS account.
* ```[suffixes]``` contains all suffixes to search for when constructing an EKS cluster's name.  If the stanza contains the entry ```company-eks-infra``` then operations will search for clusters named ```<cluster>-company-eks-infra```.  More than one entry will cause the search to be widened to incorporate more suffixes, with the first match being the one that is respected.
* ```[region]``` has one entry - the name of the AWS region that will be used.  It is likely that the code will be updated to respect (and prioritise) the ```AWS_DEFAULT_REGION``` environment variable but, at present, only the configuration file is used.

### Execution

* ```cluster show```: displays the currently selected Kubernetes cluster and current namespace.
* ```cluster list```: displays all currently configured clusters found in $HOME/.kube/config
* ```cluster use <name> [<environment>]: selects the cluster called <name>