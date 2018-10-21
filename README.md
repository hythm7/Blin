## Project Blin – Toasting Reinvented

Blin is a quality assurance tool for
[Rakudo](https://github.com/rakudo/rakudo/) releases. Blin is based on
[Whateverable](https://github.com/perl6/whateverable/).

Blin was inspired by
[Toaster](https://github.com/perl6-community-modules/perl6-Toaster). Here
are some advantages:
* Fetches archives from
  [whateverable](https://github.com/perl6/whateverable/wiki/Shareable#bot-usage-examples)
  instead of spending time to build rakudo
* Installs modules in proper order to avoid testing the same module more than once
* Deflaps modules that fail intermittently
* Automatically bisects regressed modules
* Avoids segfaults by producing no useful output instead of using DBIish


### Installation

Install required packages:
```bash
sudo apt install zstd lrzip
```

Install dependencies:

```bash
zef install --deps-only .
```

Many modules require native dependencies. See
[this page](https://github.com/perl6-community-modules/perl6-Toaster/wiki)
for the list of packages to install.


### Running

Currently it is supposed to run only on 64-bit linux systems.

If you want to test one or more modules:

```bash
PERL6LIB=lib bin/blin.p6 SomeModuleHere AnotherModuleHere
```

Here is a more practical example:

```bash
time PERL6LIB=lib START_POINT=2018.06 END_POINT=2018.09 bin/blin.p6 Foo::Regressed Foo::Regressed::Very Foo::Dependencies::B-on-A
```

If you want to test the whole ecosystem:

```bash
time PERL6LIB=lib bin/blin.p6
```

Estimated time to test the whole ecosystem with 24 cores is ≈60 minutes.

**⚠☠ SECURITY NOTE: [issues mentioned in Toaster still
apply.](https://github.com/perl6-community-modules/perl6-Toaster#warning-dangerus-stuf-ahed)
Do not run this for the whole ecosystem on non-throwaway
installs. ☠⚠**


### Viewing

See `output/overview` file for a basic overview of results. More
details for specific modules can be found in `installed/`
directory. Betters ways to view the data should come soon (hopefully).
