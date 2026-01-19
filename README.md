# Coding Conventions

## Common
Always run perlcritic with level of severity at least 3 (harsh).
If you wish to cause goodness of colleagues you can make it cruel. Try to run perlcritic with '-2' argument.
If you have a beard and a sweater or if you are Larry Wall you can start perlcritic with '-1' or '--brutal' argument. We, Our Executive nerdy, approves it.
Before start perlcritic you should run perltidy first (or in any case you will get a warning from perlcritic).

## Use this command to tidy your code:
perltidy -pro=.../.perltidyrc Ronin.pm
Or if you want to apply the changes in place (preferable option):
perltidy -pro=.../.perltidyrc -b Ronin.pm
Note the 3 dots at the beginning of the path to the profile, this means to look for this file in the current directory and in parent directories.
You can also save your own profile .perltidyrc into your home directory, but it's preferable to store it in the directory with the project (e.g. '~/svn/cdm/node/trunk/lib/perl/CDOME')

Profile "perlcritic" should contain the following minimum settings:
severity = 3
verbose = [%p] %m at line %l, column %c. %e. (Severity: %s)\n

[CodeLayout::RequireTidyCode]
perltidyrc = .perltidyrc

The minimum level of severity discussed above. Custom verbose format required to display the policy name (%p) and at the same time, reference to the page in the Canon.
Read the Canon.
And only then if you understand what is meant by a prophet and believe in what you are doing you can disable a policy or modify policy settings.
Try to read the manual pages on the policy, e.g.:
man Perl::Critic::Policy::Subroutines::RequireArgUnpacking

## Layer0
Based on Perl Best Practices book of the year 2009. With strict compliance with the rules.

## Layer1
Basic deviations from the canon (here and later PBP =  'Perl Best Practices').
Use 2 spaces for indentation instead of 4:

Code for .pertidyrc for supply this:
--indent-columns=2
--continuation-indentation=2
--nooutdent-labels
--nooutdent-keywords
Write parentheses tightly (for other type of brackets use default values). Use value 2 for this policy.
Code for .pertidyrc for supply this:
--paren-tightness=2
--square-bracket-tightness=1
--brace-tightness=1
--block-brace-tightness=0

## Layer2
Extended deviations from the canon (PBP).

The package name (as well as the package file name) in addition to the rest can begin with an underscore.
In this case the package name can start with a lowercase letter.
The package name can start with a lowercase letter.
Also this package is able to export one subroutine by default, the name of which must match the package name (without the underscore of course).
To prevent perlcritic warnings use this contruction in your code:
use base qw{Exporter};
our @EXPORT = qw{heir}; // no critic (Modules::ProhibitAutomaticExportation)

The  subroutine must begin with unpacking the formal variables, but in object-oriented methods it is allowed to postpone this procedure on one line below to separate the reference to the object.
Use the code following this pattern:

use CDOME::self;
use CDOME::error;
...
sub Init {
  my $self = &{self} or error('!self');
  my ($arg1, $arg2, @rest) = @_;
  ...

## Examples
For example, output for simple perl script:
➜ scripts git:(master) perlcritic -3 valid.pl
Code not contained in explicit package at line 1, column 1. Violates encapsulation. (Severity: 4)
Expression form of "grep" at line 6, column 9. See page 169 of PBP. (Severity: 4)
Regular expression without "/x" flag at line 6, column 20. See page 236 of PBP. (Severity: 3)
Module does not end with "1;" at line 8, column 1. Must end with a recognizable true value. (Severity: 4)
Th output warnings are point to Perl Best Practices book with description of current deviation from standart.

## Links
Oreilly Perl Best Practices Jul 2009

.perltidyrc
.perlcriticrc

## Usage

cp perltidyec ~/.perltidyrc
cp perlcritick ~/.perlcriticrc
