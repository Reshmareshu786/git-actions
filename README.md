My First GitHub Actions
This repository contains a GitHub Actions workflow that runs a Python script (addition.py) across multiple Python versions (3.8 and 3.9) using a self-hosted runner. The workflow is triggered by a push event and performs the following steps:

1.Checkout code: The workflow uses the latest version of the repository.
2.Set up Python environment: It sets up Python versions (3.8 and 3.9) as defined in the workflow matrix.
3.Install dependencies: It installs the necessary Python packages (e.g., pytest for testing).
4.Run tests: It runs the tests defined in addition.py using pytest.

How to Set Up the Self-Hosted Runner 
To use a self-hosted runner with this workflow:

1.Set up an EC2 instance (or any other server) to act as the runner. Ensure it meets the necessary system requirements for GitHub Actions runners.
2.Install the GitHub Actions runner software on the EC2 instance following GitHub's official guide.
3.Connect the runner to your GitHub repository and configure it to listen for jobs.


Running the Workflow
The workflow is triggered every time a push is made to the repository. You can also manually trigger the workflow or configure it for other events (e.g., pull requests). It will automatically:

Set up the environment for Python versions 3.8 and 3.9.
Install dependencies like pytest.
Run the pytest command to execute the tests in addition.py.

Example Workflow File
Here’s a quick look at the workflow.yml file:

name: My First GitHub Actions

on: [push]

jobs:
  build:
    runs-on: self-hosted

    strategy:
      matrix:
        python-version: [3.8, 3.9]

    steps:
    - uses: actions/checkout@v3
    - name: Set up Python
      uses: actions/setup-python@v2
      with:
        python-version: ${{ matrix.python-version }}

    - name: Install dependencies
      run: |
        python -m pip install --upgrade pip
        pip install pytest

    - name: Run tests
      run: |
        cd src
        python -m pytest addition.py

How to Add More Tests ?
1.Create Python test files in the src directory.
2.Use the pytest testing framework to write your unit tests.
3.The workflow will automatically discover and run any tests you write.
