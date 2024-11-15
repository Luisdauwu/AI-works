name: CI with Snyk and CodeQL

on:
  push:
    branches:
      - main
  pull_request:

jobs:
  snyk-scan:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Set up Snyk
        uses: snyk/actions@master
        env:
          SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}

      - name: Test Dockerfile for vulnerabilities
        run: snyk container test --file=Dockerfile

