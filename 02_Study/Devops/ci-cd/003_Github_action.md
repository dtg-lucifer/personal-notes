### Example workflows for #snappy-notes 

This is a example workflow for the CI CD pipeline for the project #snappy-notes 
- Steps of the CI job
	- [ ] Checkout the code from the repo
	- [ ] install the necessary dependencies
	- [ ] Run lint and tests to see if there is any error or not
	- [ ] OF everything is fine therefore it will invoke the CD job
		- [ ] Which therefore build the docker image out of the checked out code 
		- [ ] Push that image to the repository

```yml
name: CI_DEV

on:
  workflow_dispatch:
  push:
    branches-ignore:
      - master
      - main
      - release
      - release-*
      - v*
  pull_request:
    branches:
      - main
      - master
      - dev
      - dev-*
      - feature-*

jobs:
  lint-format-test:
    runs-on: ubuntu-latest
    environment: build

    steps:
      - name: Checkout code
        uses: actions/checkout@v3
  
      - name: Set up Node.js
        uses: actions/setup-node@v3
        with:
          node-version: "20.11.0"

      - name: Install dependencies
        run: npm install
        shell: bash

      - name: Testing and linting
        uses: ./.github/actions/tests
        with:
          silent_test: false
          fix_lint: false
```

This depends on the following **Composite action**

```yml
name: Test and Lint Project
description: 'Runs Prettier, ESLint, and unit tests.'

inputs:
  silent_test:
    description: 'Run tests in silent mode.'
    required: false
    default: 'false'
  fix_lint:
    description: 'Fix linting errors.'
    required: false
    default: 'false'

runs:
  using: composite
  steps:
    - name: Run Prettier
      run: npm run format
      shell: bash
  
    - name: Run ESLint
      if: ${{ inputs.fix_lint == 'true' }}
      run: npm run lint:fix
      shell: bash
      env:
        CI: true

    - name: Run ESLint (without fix)
      if: ${{ inputs.fix_lint != 'true' }}
      run: npm run lint
      shell: bash
      env:
        CI: true

    - name: Run unit tests (silent mode)
      if: ${{ inputs.silent_test == 'true' }}
      run: npm run test:silent
      shell: bash
      env:
        CI: true
  
    - name: Run unit tests (normal mode)
      if: ${{ inputs.silent_test != 'true' }}
      run: npm run test
      shell: bash
      env:
        CI: true
```

### What does this workflow do ???
This workflow simply watched for any push on the branches other than ***main, master, release-\*, v\****, and also watches for any pull requests which are requested for for the branches like ***master, main, dev, dev-\*, feature-\****, and after invoking the workflow it just simply check for any linting errors and tests out the whole code base and report back. 

Where as the other production workflow wathes for only pushes in the master branch and in case that happens it simply build the docker image based on the **Dockerfile** and pushes that to the **docker-hub** registry

The workflow for the production one is the same just the composite action for building the docker image and pushing that is different

```yml
name: 'Build and Push Docker Image'
description: 'Builds and pushes a Docker image with a version tag.'

inputs:
  docker_username:
    description: 'Docker username'
    required: true
  docker_password:
    description: 'Docker password'
    required: true
  docker_registry:
    description: 'Docker registry URL (e.g., docker.io for Docker Hub)'
    required: true
  repository:
    description: 'Repository name for Docker image'
    required: true

runs:
  using: 'composite'
  steps:
    - name: Log in to Docker
      run: |
        echo "${{ inputs.docker_password }}" | docker login -u ${{ inputs.docker_username }} --password-stdin
      shell: bash
  
    - name: Build Docker image
      run: |
        VERSION=$(git rev-list --count HEAD)
        docker build -t ${{ inputs.docker_registry }}/${{ inputs.repository }}:${VERSION} .
      shell: bash

    - name: Push Docker image
      run: |
        VERSION=$(git rev-list --count HEAD)
        docker push ${{ inputs.docker_registry }}/${{ inputs.repository }}:${VERSION}
      shell: bash
```
