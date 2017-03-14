# Packaging

## Debian Packaging

To create an Ansible Debian DEB packages:

```
vagrant up debian
vagrant ssh debian
```

After you ssh you should be automatically navigated into ```/go/src/github.com/pearsonappeng/tensor/``` directory, If not change directory using ```cd /go/src/github.com/pearsonappeng/tensor/```.

__Note__: You must run this target as root or set `export PBUILDER_BIN='sudo pbuilder'`

```
DEB_DIST='jessie' make deb
```

The debian package file will be placed in the `deb-build` directory. This can then be added to an APT repository or installed with `dpkg -i <package-file>`.

Note that `dpkg -i` does not resolve dependencies.

To install the Tensor DEB package and resolve dependencies:

```
dpkg -i <package-file>
apt-get -fy install
```

Or, if you are running Debian Stretch (or later):

```
apt install /path/to/<package-file>
```

To create an Ansible Ubuntu DEB packages:

```
vagrant up ubuntu --provider virtualbox
vagrant ssh ubuntu
```

After you ssh you should be automatically navigated into ```/go/src/github.com/pearsonappeng/tensor/``` directory, If not change directory using ```cd /go/src/github.com/pearsonappeng/tensor/```.

__Note__: You must run this target as root or set `export PBUILDER_BIN='sudo pbuilder'`

```
DEB_DIST='xenial trusty precise' make deb
```

The debian package file will be placed in the `deb-build` directory. This can then be added to an APT repository or installed with `dpkg -i <package-file>`.

Note that `dpkg -i` does not resolve dependencies.

To install the Tensor DEB package and resolve dependencies:

```
apt-get -fy install
```

Or, if you are running Ubuntu Xenial (or later):

```
apt install /path/to/<package-file>
```

## RPM Packaging

To create an Ansible RPM package:

```
vagrant up centos
vagrant ssh centos
```

After you ssh you should be automatically navigated into ```/go/src/github.com/pearsonappeng/tensor/``` directory, If not change directory using ```cd /go/src/github.com/pearsonappeng/tensor/```.

```
make rpm
```

The rpm package file will be placed in the `rpm-build` directory. This can then be added to an RPM repository or installed with `rpm -i <package-file>`.

Note that `rpm -i` does not resolve dependencies.

To install the Tensor RPM package and resolve dependencies:

```
yum -y install
```

Or, if you are running Fedora 18 (or later):

```
dnf install /path/to/<package-file>
```

## Building Docker

```vagrant up debian``` ```vagrant up centos``` or ```vagrant up ubuntu --provider virtualbox```

and 

``vagrant ssh [os]``

After you ssh you should be automatically navigated into ```/go/src/github.com/pearsonappeng/tensor/``` directory, If not change directory using ```cd /go/src/github.com/pearsonappeng/tensor/```.

```
make build-docker-image
```