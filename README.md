# Rust Codecov

<p align="center">
    <img alt="docker" src="http://iron-oxide.gitlab.io/icons/logos/docker.svg" width="100" height="100" /> <img alt="rust" src="http://iron-oxide.gitlab.io/icons/logos/rust.svg" width="100" height="100" /> <img alt="codecov" src="http://iron-oxide.gitlab.io/icons/logos/codecov.svg" width="100" height="100" />
</p>

[Official Rust](https://hub.docker.com/_/rust/) with requirements for Codecov. All builds are automated so they are always the most recent images.

## Usage

All of the images can be found in the project [registry](https://gitlab.com/iron-oxide/docker/rust-codecov/container_registry) and can be used just like images from dockerhub.

    docker pull registry.gitlab.com/iron-oxide/docker/rust-codecov:stable
    docker pull registry.gitlab.com/iron-oxide/docker/rust-codecov:beta
    docker pull registry.gitlab.com/iron-oxide/docker/rust-codecov:nightly

To use with CI just replace `image: rust` with the URL of the registry image.
