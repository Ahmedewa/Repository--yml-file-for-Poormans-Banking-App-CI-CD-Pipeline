# Repository--yml-file-for-Poormans-Banking-App-CI-CD-Pipeline
Repository for "Poormans Bank" App (.yml file)      .YAML file:

yaml
name: Poormans Bank CI/CD

on:
  push:
    branches:
      - main

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Set up Docker Buildx
        uses: docker/setup-buildx-action@v1

      - name: Build Docker image
        run: docker build -t poormansbank .

      - name: Run Docker container
        run: docker run -p 8080:8080 poormansbank

      - name: Deploy to Jira Cloud
        run: jira cloud deploy --cluster poormansbank --service poormansbank
