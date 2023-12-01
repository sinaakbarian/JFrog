# JFrog Artifactory

## What is Artifactory?

JFrog Artifactory is a centralized repository platform designed to streamline the automation and management of binaries and artifacts throughout the application delivery process. It serves as a comprehensive solution for end-to-end DevOps, offering support for various package registries such as Maven, NuGet, NPM, PyPi, Pip, Docker, and more. Users can seamlessly upload and download artifacts to and from their environments.

## Problem Solving Steps

1. **Developer Commit:**
   - Developers commit code to GitHub.

2. **CI/CD Trigger:**
   - The CI/CD server, such as Jenkins, is triggered.

3. **Unit Testing:**
   - The code undergoes unit testing.

4. **Artifactory Upload:**
   - Upon successful testing, the results are pushed to JFrog Artifactory.

5. **User Access:**
   - Users can pull the artifacts from JFrog Artifactory for further development.

## History

JFrog is an end-to-end DevOps solution, and Artifactory is a key component. It is not just a container for images; it also encompasses JFrog Pipelines for next-gen CI/CD. JFrog Pipelines further enhance reproducibility, making the entire development process more manageable.

## Why JFrog?

JFrog provides an all-encompassing solution for managing artifacts, ensuring that the software development lifecycle is seamless. Its support for various package registries, combined with JFrog Pipelines, makes it a preferred choice for DevOps.

## Getting Started

1. Visit [JFrog Artifactory](https://takedaawsuseast.jfrog.io/) to log in.
2. Set up your account as provided to you.

## Connecting to JFrog in GitHub Actions

Add the following to your GitHub Actions workflow files:

```yaml
- uses: jfrog/setup-jfrog-cli@v3
  env:
    # JFrog platform URL (e.g., https://acme.jfrog.io)
    JF_URL: ${{ secrets.JF_URL }}
    
    # Basic authentication credentials
    JF_USER: ${{ secrets.JF_USER }}
    JF_PASSWORD: ${{ secrets.JF_PASSWORD }}
    # or
    # JFrog Platform access token
    JF_ACCESS_TOKEN: ${{ secrets.JF_ACCESS_TOKEN }}

- run: |
    jf rt ping
    jf rt dl artifacts/
    jf rt u aether artifacts/
    jf rt bp

- run: |
    docker login ${{ secrets.DOCKER_REGISTRY_URL }} -u ${{ secrets.DOCKER_USERNAME }} -p ${{ secrets.DOCKER_PASSWORD }}
    docker tag your_docker_image:tag ${{ secrets.JF_URL }}/your_artifactory_repository/your_docker_image:tag
    docker push ${{ secrets.JF_URL }}/your_artifactory_repository/your_docker_image:tag
```

Note: Replace placeholders like `your_docker_image:tag` and customize according to your setup.

Feel free to explore other container registries, but JFrog Artifactory stands out for its simplicity and efficiency in managing artifacts throughout the development lifecycle.
