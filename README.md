# Fyne Cross

[![CircleCI](https://circleci.com/gh/lucor/fyne-cross.svg?style=svg)](https://circleci.com/gh/lucor/fyne-cross) [![Go Report Card](https://goreportcard.com/badge/github.com/lucor/fyne-cross)](https://goreportcard.com/report/github.com/lucor/fyne-cross) [![GoDoc](https://godoc.org/github.com/lucor/fyne-cross?status.svg)](http://godoc.org/github.com/lucor/fyne-cross) [![GitHub tag](https://img.shields.io/github/tag/lucor/fyne-cross.svg)]()

fyne-cross is a simple tool to cross compile [Fyne](https://fyne.io) applications.

It has been inspired by [xgo](https://github.com/karalabe/xgo) and uses a [docker image](https://hub.docker.com/r/lucor/fyne-cross) built on top of the [golang-cross](https://github.com/docker/golang-cross) image,
that includes the MinGW compiler for windows, and an OSX SDK, along the Fyne requirements.

Supported targets are:
  -  darwin/amd64
  -  darwin/386
  -  linux/amd64
  -  linux/386
  -  linux/arm
  -  linux/arm64
  -  windows/amd64
  -  windows/386

## Requirements

- go
- docker

## Installation

        go get github.com/lucor/fyne-cross

### Development release

To install a preview of the next version or help in testing:

        go get github.com/lucor/fyne-cross@develop
        
if you make changes in the code this will build the command:

        go build -o $GOPATH/bin/fyne-cross *.go
        
## Pre-requirement if you use/import private repos

Create a folder `.fyne-cross` in your home directory, it will be mapped into the docker machines as /home/fyne
so you can create on it a `.gitconfig` file with these contents (ex.gitlab)
        
```
[user]
    name = Write here your name
    email = Write here your email
[url "git@gitlab.com:"]
    insteadOf = https://gitlab.com/
```

also you can create a `.ssh` folder and copy over it your `~/.id_rsa.pub` or whatever indentity file 
you use to deal with your private repo

in order to map this folder you should use --home when invoke fyne-cross

## Usage

        fyne-cross --targets=linux/amd64,windows/amd64,darwin/amd64 package

> Use `fyne-cross help` for more informations

### Wildcards

The `targets` flag support wildcards in case want to compile against all supported GOARCH for a specified GOOS

Example:

        fyne-cross --targets=linux/*

is equivalent to

       fyne-cross --targets=linux/amd64,linux/386,linux/arm64,linux/arm

## Example

The example below cross build the [fyne examples application](https://github.com/fyne-io/examples)

        git clone https://github.com/fyne-io/examples.git
        cd examples
        fyne-cross --targets=linux/amd64,windows/amd64,darwin/amd64 github.com/fyne-io/examples

Builds for the specified targets will be available under the `build` folder

## Contribute

- Fork and clone the repository
- Make and test your changes
- Open a pull request against the `develop` branch

### Contributors

See [contributors](https://github.com/lucor/fyne-cross/graphs/contributors) page
