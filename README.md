# dashboard
Simple dashboard for monitoring CPAN modules

## Simple Set-Up

To configure this system to work with your system, do the following:

* Register with Travis-CI and Coveralls using your Github login
* Activate the repos that you want to report on in both Travis-CI and Coveralls
* Add the simple .travis.yml file to your repos
* Edit the `dashboard.json` file so it is configured correctly
* Push changes to your repos
* Run `dashboard`

**Note:** For (slightly) more detail about setting up Travis-CI and Coveralls, see [my presentation on the subject]
(http://www.slideshare.net/davorg/github-travisci-and-perl).

## Sample .travis.yml

A simple .travis.yml for a a CPAN module looks like this.

    language: perl
    perl:
      - "5.12"
      - "5.14"
      - "5.16"
      - "5.18"
      - "5.20"

    before_install:
      cpanm -n Devel::Cover::Report::Coveralls
    script:
      perl Build.PL && ./Build build && cover -test -report coveralls

This works well for most of my CPAN modules.

## Configuration

You configure the system by editing `dashboard.json`. There are three main sections in the file.

* **modules** - a list of the modules that you want to monitor. Each module has up to three pieces of information
associated with it.
  * **name** - the name of the module (more accurately, the name of the most important module in the distribution).
  This is required.
  * **dist** - the name of the distribution. This can be omitted, in which case it is synthesised by converting
  all `::` in the name to `-`.
  * **repo** - the name of the Github repo. This can be omitted, in which case it is synthesises by converting the
  dist value to lower case.
* **author** - information about the author of the modules.
  * **github** - your Github username.
  * **cpan** - your CPAN username.
* **output** - various output parameters
  * **file** - the name of the output file.
  * **template** - the name of the input template.
  * **title** - the title to use on the output page.
  * **about** - a link to an "about" page. If this omitted, then the "about" link is omitted from the navbar.
  * **analytics** - a Google Analytics code. If this is given, then a Google Analytics section is added to the output.

## Example

You can see this code in action at http://code.perlhacks.com/.