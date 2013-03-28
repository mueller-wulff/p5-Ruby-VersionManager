# NAME

Ruby::VersionManager

# WARNING!

This is an unstable development release not ready for production!

# VERSION

Version 0.003019

# SYNOPSIS

The Ruby::VersionManager Module will provide a subset of the bash rvm.

Ruby::VersionManager comes with a script rvm.pl. See the perldoc of rvm.pl for a list of actions and options.

# ATTRIBUTES

## rootdir

Root directory for Ruby::VersionManager file structure.

## ruby\_version

The ruby version to install, check or remove.
Any String matching one of the major ruby versions is valid. Ruby::VersionManager will guess a version based on available versions matching the string. If multiple versions match the latest stable release will be used.
Preview and RC versions will never be installed automatically. You have to provide the full matching version string as shown with the list method.

## gemset

Name your gemset. More sophisticated support for gemsets needs to be implemented.

## gem

Uses Ruby::VersionManager::Gem to pass arguments to the 'gem' command.
Additionally you can resemble gemsets from other users or machines by using reinstall with a file containing the output of 'gem list'. When omiting the file name the currently installed gemset will be completely reinstalled without pulling in any additional dependencies.

    $rvm->gem('reinstall', ($filename)); # install all gems given in the file
    $rvm->gem('reinstall');              # reinstall all gems from the currently used gemset

    $rvm->gem('install', ('unicorn', '-v=4.0.1));   # install unicorn. Same as 'gem install unicorn -v=4.0.1' on the command line

## agent\_string

The user agent used when downloading ruby.
Defaults to Ruby::VersionManager/0.003019.

## archive\_type

Type of the ruby archive to download.
Defaults to .tar.bz2, valid are also .tar.gz and .zip.

## major\_version

Will be automatically set.

## rubygems\_version

Not yet in use.

# CONSTRUCTION

All attributes are optional at creation. Note that rootdir should be set at construction if you want another directory than default because Ruby::VersionManager->new will bootstrap the needed directories.

    my $rvm = Ruby:VersionManager->new;

Or

    my $rvm = Ruby:VersionManager->new(
        rootdir => '/path/to/root',
        ruby_version => '1.8',
        gemset => 'name_of_the_set',
    );



# METHODS

## available\_rubies

Returns a hashref of the available ruby versions.

## installed\_rubies

Returns a hashref of the installed ruby versions.

## list

Print a list of available and installed ruby versions to STDOUT.

    $rvm->list;

## updatedb

Update database of available ruby versions.

    $rvm->updatedb;

## install

Install a ruby version. If no version is given the latest stable release will be installed.
The program tries to guess the correct version from the provided string. It should at least match the major release.
If you need to install a preview or rc version you will have to provide the full exact version.

Latest ruby

    $rvm->ruby_version('1.9');
    $rvm->install;

Latest ruby-1.8

    $rvm->ruby_version('1.8');
    $rvm->install;

Install preview

    $rvm->ruby_version('ruby-1.9.3-preview1');
    $rvm->install;

## uninstall

Remove a ruby version and the source dir including the downloaded archive.
You have to provide the full exact version of the ruby you want to remove as shown with list.

    $rvm->ruby_version('ruby-1.9.3-preview1');
    $rvm->uninstall;

## switch\_gemset

Update the environment to use another gem set for the corrently active ruby.

    $rvm->switch_gemset('another_set')

# LIMITATIONS AND TODO

Currently Ruby::VersionManager is only tested to be running on Linux with bash installed.
Better support of gemsets needs to be added.

# AUTHOR

Mugen Kenichi, `<mugen.kenichi at uninets.eu>`

# BUGS

Report bugs at:

- Ruby::VersionManager issue tracker

    [https://github.com/mugenken/p5-Ruby-VersionManager/issues](https://github.com/mugenken/p5-Ruby-VersionManager/issues)

- support at uninets.eu

    `<mugen.kenichi at uninets.eu>`

# SUPPORT

- Technical support

    `<mugen.kenichi at uninets.eu>`
