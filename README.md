# Potassium

[![ion install loglib](https://img.shields.io/badge/ion%20install-potassium-blue.svg)](https://github.com/IodineLang/Ion)
![version v0.1.0](https://img.shields.io/badge/version-v0.1.0-blue.svg)
![deps](https://img.shields.io/badge/dependencies-loglib%20v0.1.0-blue.svg)

Potassium is a powerful, flexible and downright awesome web framework for the [Iodine](https://github.com/IodineLang/Iodine)
programming language. Potassium aims to help accelerate the development of your website by providing convenient, flexible base 
classes which take away unnecessary boilerplate and reduces the risk of errors or vulnerabilities.

## Installing
Potassium's really easy to install through [Ion](https://github.com/IodineLang/Ion). We recommend that you install it globally 
so that your CGI server can also load the Potassium libraries. To do this, simply type:

    sudo ion install --global potassium

Alternatively, you can just copy the `src/potassium` folder to your project's source directory, and Iodine will automatically 
use it as a module.

## Features
- Function-based views system
- Powerful URL router, similar to **AngularJS**
- HTML, JSON and Template responses for views
- Iodine-based templating language (created by @GruntTheDivine)
- GET and POST data handling (supports `application/json` and `application/x-www-form-urlencoded` data, but not `multipart/form-data`)

## Documentation
See the [`docs`](https://github.com/IodineLang/Potassium/tree/master/docs) folder for documentation on all key features of 
Potassium. 

## Coding Style and Contributions
All contributions **must** comply with the [style guide](https://github.com/IodineLang/Iodine/wiki/Aurora01's-Style-Guide)
for Iodine. Semicolons are **always** used. Line length should stay under 80 characters, and no line should be over 100 
characters.
