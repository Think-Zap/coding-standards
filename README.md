# Zap Coding Standards

The Zap Coding Standard is a set of [PHP_CodeSniffer](https://github.com/squizlabs/PHP_CodeSniffer) rules for use primarily with the Zap Competition plugins.

## Requirements

- PHP ^7.4

## Install

Composer v2:

```bash
composer require --dev Think-Zap/coding-standards "^1.0"`
```

Composer v1:

Add to the `repositories` object:

```json
    {
      "type": "vcs",
      "url": "git@github.com:Think-Zap/coding-standards.git"
    }
```

And `require-dev`:

```json
  "Think-Zap/coding-standards": "^3.0"
```

## Project ruleset

> Ensure you're running PHP 7.4 locally!

To use this ruleset, create a `phpcs.xml.dist` in the root of the project and add the following content:

```xml
<?xml version="1.0"?>
<ruleset>
	<arg name="basepath" value="." />
	<arg name="extensions" value="php" />
	<arg name="severity" value="4" />
	<arg name="tab-width" value="4" />
	<arg name="parallel" value="80" />
	<arg name="colors" />

	<!--  Update to the PHP version your production/local docker container runs on -->
	<config name="testVersion" value="7.4" />
	<!-- php -r 'echo PHP_VERSION_ID;' -->
	<config name="php_version" value="70400" />

	<!-- Fix WordPress's terrible typing breaking PHPCS -->
	<config name="minimum_supported_wp_version" value="5.6.0" />

	<!-- Ignore warnings, show progress of the run and show sniff names -->
	<arg value="nps" />

	<!-- Directories to be checked -->
	<file>./wp-content/plugins</file>

	<!-- Exclude files -->
	<exclude-pattern>*-config.php</exclude-pattern>
	<exclude-pattern>*vendor/</exclude-pattern>
	<exclude-pattern>*tests/*</exclude-pattern>
	<exclude-pattern>*.twig</exclude-pattern>
	<exclude-pattern>*webpack/</exclude-pattern>

	<!-- Include the Zap coding standard -->
	<rule ref="Zap" />
</ruleset>
```

> Add `phpcs.xml` to your `.gitignore`

## Manual Usage

**PHPCS**
```bash
./vendor/bin/phpcs --standard=Zap /path/to/files/**.php
```

**PHPCBF**
```bash
./vendor/bin/phpcbf --standard=Zap /path/to/files/**.php
```
