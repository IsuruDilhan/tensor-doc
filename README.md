<p align="center">
  <img src="source/images/logo.png?raw=true" alt="Tensor: Documentation" width="226">
  <br>
  <a href="https://travis-ci.org/pearsonappeng/tensor-doc"><img src="https://travis-ci.org/pearsonappeng/tensor-doc.svg?branch=master" alt="Build Status"></a>
</p>

<p align="center">Tensor documentation.</p>

Contribute
------------------------------

### Prerequisites

You're going to need:

 - **Linux or OS X** — Windows may work, but is unsupported.
 - **Ruby, version 2.2.5 or newer**
 - **Bundler** — If Ruby is already installed, but the `bundle` command doesn't work, just run `gem install bundler` in a terminal.

### Getting Set Up

1. Clone this repository to your hard drive with `git clone https://github.com/pearsonappeng/tensor-doc.git`
2. `cd tensor-doc`
3. Initialize and start tensor-doc. You can either do this locally, or with Vagrant:

```shell
# either run this to run locally
bundle install
bundle exec middleman server

# OR run this to run with vagrant
vagrant up
```

You can now see the docs at http://localhost:4567. Whoa! That was fast!