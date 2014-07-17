[![alt tag](http://img.shields.io/badge/maintainer-hawkinswnaf-blue.svg)](https://github.com/hawkinswnaf)

# commotion-translation-generator
=============================================

## Summary
Parses commotion-router source files for user-facing strings and uses them to generate PO files for [https://github.com/opentechinstitute/luci-i18n-commotion](luci-i18n-commotion). The PO file generator will attempt to re-use any existing translations in the new PO file.

Translation of Commotion Router is managed on Transifex:
https://www.transifex.com/projects/p/commotion-user-interface/

## Prerequisites
* Perl 5
* perl modules ([available through cpan](http://www.cpan.org/modules/INSTALL.html))
  * DateTime
  * File::Copy
  * File::Next
  * File::Path
  * Git::Repository
  * Text::Balanced

## Setup and Usage

1. Install perl.
2. Install prerequisite modules:
  a. From a terminal prompt, install cpanm (`cpan App::cpanm`).
  b. Use cpanm to install modules (e.g., `cpanm File::Copy`).
3. Change to the scripts directory (`cd scripts`).
4. Run `parse.pl`. Newly generated PO files will be written to `scripts/working/translations/` and must be manually added to luci-i18n-commotion for upload to github.


## PO Files
Commotion-Router uses LuCI's i18n API and PO file system to manage system language. Any user-facing text in a LuCI model, view, or controller file may be marked translatable using standard tags (i.e., `translate("some text")`, `translatef("formatted text: %d", var)` for code or `<%:some text%>` for templates). Translatable text will then be checked against the active system language file (PO file). If an exact match is found, the page will be rendered using the PO file's translation for that string. If no match is found, or if the string has not yet been translated, the page will be rendered using the original text.

Each PO file uses a standard header containing translation project metadata, followed by origin/translation string pairs.

### PO File Header Format
PO file header structure is as follows (using Commotion Router's French translation as an example).

```
"Project-Id-Version: Commotion User Interface\n"
"Report-Msgid-Bugs-To: \n"
"POT-Creation-Date: 2013-08-01 02:43+0500\n"
"PO-Revision-Date: 2013-11-20 10:05+0000\n"
"Last-Translator: st\n"
"Language-Team: French (http://www.transifex.com/projects/p/commotion-user-interface/language/fr/)\n"
"MIME-Version: 1.0\n"
"Content-Type: text/plain; charset=UTF-8\n"
"Content-Transfer-Encoding: 8bit\n"
"Language: fr\n"
"Plural-Forms: nplurals=2; plural=(n > 1);\n"
```

### PO File Translation Format
PO file origin/translation string pairs are designated as follows.

```
msgid "Access Point Name"
msgstr "Nom du point d'accès"
```