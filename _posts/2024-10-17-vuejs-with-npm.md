---
layout: post
title: VueJS with NPM
date: 2024-10-17 10:22 +0200
categories: [VueJS, Frontend]
tags: [VueJS, npm]
description: Getting Started with VueJS and npm.
---
# Getting Started with VueJS and npm

VueJS is a JavaScript framework that is used to build interactive web applications.
It is a progressive framework that can be used to build single-page applications.
VueJS is a popular choice for developers because of its simplicity and ease of use.
npm is a package manager for JavaScript that is used to install and manage packages.
In this tutorial, we will learn how to get started with VueJS using npm.

## Setup Project

```shell
npm create vue@latest
```

This command will create a new VueJS project in the current directory.
You will be prompted to answer a few questions about the project, such as the project name and the package manager to use.
```shell
✔ Project name: … <your-project-name>
✔ Add TypeScript? … No / Yes
✔ Add JSX Support? … No / Yes
✔ Add Pinia for state management? … No / Yes
✔ Add Vitest for Unit testing? … No / Yes
✔ Add an End-to-End Testing Solution? … No / Cypress / Nightwatch / Playwright
✔ Add ESLint for code quality? … No / Yes
✔ Add Prettier for code formatting? … No / Yes
✔ Add Vue DevTools 7 extension for debugging? (experimental) … No / Yes
```

After answering the questions, the project will be created.

## Run Project

```shell
cd <your-project-name>
npm install
npm run serve
```

This will install the necessary dependencies and start the development server.

## Ready for Production

To build the project for production, run the following command:
```shell
npm run build
```
This will create a `dist` directory with the production-ready files.

## Further Reading
[VueJS Guide](https://vuejs.org/guide/quick-start.html)
