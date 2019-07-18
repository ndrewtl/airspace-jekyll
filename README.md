# _Airspace_ for Jekyll
![screenshot](screenshots/home.png "Description goes here")

This Jekyll theme is a port of [ThemeFisher's](https://themefisher.com) [Airspace template](https://themefisher.com/products/airspace-free-bootstrap-website-template/). It is released under ThemeFisher's [license](https://themefisher.com/license) , which requires attribution. Concern about the licnese please contact with [them](mailto:themefisher@gmail.com)

## Usage
To start your project, [fork this respository](https://github.com/ndrewtl/airspace-jekyll/fork), put in your content, and go!

## Examples
Here are some projects that have used this Jekyll Theme:
* [BOYUAN Open Source 博辕开源](https://boyuanitsm.github.io)
* [Campus VC](https://mrchildneo.github.io/mrchildneo/)
* [Mãos de amar](https://www.maosdeamar.com.br/)
* [ATK Team](http://www.atksec.com/)
* [Coding Club](https://ourcodingclub.github.io/)
* [Dev Empathy Book Club](http://www.devempathybook.club/)
* [DKAN Open Data Catalog](http://getdkan.com) (modified version of this theme)

## Steps for Setup:

### Make sure you have Ruby

First, make sure you have [Ruby](https://www.ruby-lang.org/en/) installed. You can confirm this by running `ruby -v` on the command line:

```sh
$ ruby -v
ruby [version number] (date) [your platform]
```

If you get something like `"Error, command not found"` visit the link above and
install Ruby for your platform.


### Make sure you have Bundler

Next, make sure you have [Bundler](https://bundler.io) installed. Just like
above, run `bundle -v` on the command line:

```sh
$ bundle -v
bundle [version number]
```

If you get `"Error, command not found"` run `gem install bundler` to install it
using RubyGems.

### Run this repository

Clone the repository, and `cd` into it:
```sh
$ git clone https://github.com/ndrewtl/airspace-jekyll.git
$ cd airspace-jekyll
```

Install dependencies locally:
```sh
$ bundle install --path vendor/bundle
```

This should install a local copy of jekyll.

Now run the server:
```sh
$ ./vendor/bundle/ruby/#{YOUR_RUBY_VERSION}/bin/jekyll server
```
