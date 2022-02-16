# Lint-project

# Let’s set up a simple project to see how it works!

npm init -y

#Install ESLint. ESLint is a tool for identifying and reporting on patterns found in JavaScript code.

npm install eslint -DE

ESLint configuration file example:

# .eslintrc.yml

env:
es2021: true
browser: true

extends:
- eslint:recommended

parserOptions:
ecmaVersion: 2021
sourceType: module

// scripts in package.json

{
 "scripts": {
 "lint:js": "eslint src/**/*.js",
 "lint": "npm run lint:js"
 }
}

# .github/workflows/lint.yml

name: Lint # name of the action (displayed in the github interface)

on: # event list
pull_request: # on a pull request to each of these branches
branches:
- development
- staging
- production

env: # environment variables (available in any part of the action)
NODE_VERSION: 14

jobs: # list of things to do
linting:
name: Linting # job name (unique id)
runs-on: ubuntu-latest # on which machine to run
steps: # list of steps
- name: Install NodeJS
uses: actions/setup-node@v2
with:
node-version: ${{ env.NODE_VERSION }}

- name: Code Checkout
uses: actions/checkout@v2

- name: Install Dependencies
run: npm ci

- name: Code Linting
run: npm run lint
