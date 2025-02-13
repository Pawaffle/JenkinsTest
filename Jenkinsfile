#!/bin/bash

# Exit on any failure
set -e

# Define repository URL
REPO_URL="https://github.com/Pawaffle/JenkinsTest.git"
WORKDIR="jenkins-test-workspace"

# Function to print stage headers
print_stage() {
    echo
    echo "====================================="
    echo " STAGE: $1"
    echo "====================================="
}

# Cleanup previous workspace if it exists
rm -rf "$WORKDIR"
mkdir "$WORKDIR"
cd "$WORKDIR"

# Stage 1: Checkout
print_stage "Checkout"
git clone "$REPO_URL" .
echo "Repository cloned successfully."

# Stage 2: Build
print_stage "Build"
mvn clean install
echo "Build completed."

# Stage 3: Test
print_stage "Test"
mvn test
echo "Tests completed."

# Stage 4: Code Coverage
print_stage "Code Coverage"
mvn jacoco:report
echo "Code coverage report generated."

# Post-processing
print_stage "Post-processing"
if ls target/surefire-reports/*.xml 1> /dev/null 2>&1; then
    echo "JUnit test reports found:"
    ls target/surefire-reports/*.xml
else
    echo "No JUnit test reports found."
fi

if ls target/site/jacoco/index.html 1> /dev/null 2>&1; then
    echo "JaCoCo coverage report generated at target/site/jacoco/index.html"
else
    echo "JaCoCo coverage report not found."
fi

echo "Pipeline execution completed successfully!"
