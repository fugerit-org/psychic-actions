# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Changed

- java-type parameter deprecated as now graalvm is handled by <https://github.com/actions/setup-java>
- [maven-build-scan] added parameter : maven-additional-options

## [1.3.2] - 2024-09-16

### Changed 

- [maven-build-scan] added parameter : maven-additional-options

### Fixed

- snyk args to docker build

## [1.3.1] - 2024-08-04

### Changed

- [maven-build-scan] enable-maven-dependency-submission property substitutes disable-maven-dependency-submission
  (now the default behaviour is not sending dependency graph)
- [maven-build-scan] disable-maven-dependency-submission is deprecated (will be ignore)

## [1.3.0] - 2024-04-22

### Added

- [Maven container publish GitHub action](maven-container-publish/maven-container-publish.md)

## [1.2.1] - 2024-04-15

### Changed

- Added 'disable-upload-sarif' parameter to [Maven build and scan GitHub action](maven-build-scan/maven-build-scan.md)

## [1.2.0] - 2024-03-18

### Changed

- Added 'maven-core' parameter to [Maven build and scan GitHub action](maven-build-scan/maven-build-scan.md)

## [1.1.0] - 2024-02-22

### Changed

- Added snyk parameters to action [Maven build and scan GitHub action](maven-build-scan/maven-build-scan.md)

## [1.0.0] - 2024-02-21

### Added

- [Maven build and scan GitHub action](maven-build-scan/maven-build-scan.md)
