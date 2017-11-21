# Rust Codecov

Stable: [![pipeline status](https://gitlab.com/starshell/docker/rust-codecov/badges/stable/pipeline.svg)](https://gitlab.com/starshell/docker/rust-codecov/commits/stable) Beta: [![pipeline status](https://gitlab.com/starshell/docker/rust-codecov/badges/beta/pipeline.svg)](https://gitlab.com/starshell/docker/rust-codecov/commits/beta) Nightly: [![pipeline status](https://gitlab.com/starshell/docker/rust-codecov/badges/nightly/pipeline.svg)](https://gitlab.com/starshell/docker/rust-codecov/commits/nightly)

<p align="center">
    <img alt="docker" src="http://iron-oxide.gitlab.io/icons/logos/docker.svg" width="100" height="100" /> <img alt="rust" src="http://iron-oxide.gitlab.io/icons/logos/rust.svg" width="100" height="100" /> <img alt="codecov" src="http://iron-oxide.gitlab.io/icons/logos/codecov.svg" width="100" height="100" />
</p>

[Official Rust](https://hub.docker.com/_/rust/) with requirements for Codecov. All builds are automated so they are always the most recent images. The nightly image rebuilds every day, both beta and nightly rebuild once a week.

## Usage

The images are hosted on both Dockerhub and GitLab registries. While I have not tested it, if using GitLab CI, those images will likely be much faster.

### Dockerhub

To use the [dockerhub registry](https://hub.docker.com/r/datenstrom/rust-codecov/), the `datenstrom/rust-codecov` image. The `stable`, `beta`, and `nightly` tags are available.

    docker pull datenstrom/rust-codecov:stable
    docker pull datenstrom/rust-codecov:beta
    docker pull datenstrom/rust-codecov:nightly

### GitLab

All of the images can be found in the project [registry](https://gitlab.com/starshell/docker/rust-codecov/container_registry) and can be used just like images from dockerhub.

    docker pull registry.gitlab.com/starshell/docker/rust-codecov:stable
    docker pull registry.gitlab.com/starshell/docker/rust-codecov:beta
    docker pull registry.gitlab.com/starshell/docker/rust-codecov:nightly

To use with CI just replace `image: rust` with the URL of the registry image.

    .cargo_test_template: &cargo_test
      stage: test
      script:
        - cargo test --verbose --jobs 1 --all

    test:stable:cargo:
      image: registry.gitlab.com/starshell/docker/rust-codecov:stable
      <<: *cargo_test
      after_script:
        - |
          for file in target/debug/question-*[^\.d]; do mkdir -p "target/cov/$(basename $file)"; kcov --exclude-pattern=/.cargo,/usr/lib --verify "target/cov/$(basename $file)" "$file"; done &&
          bash <(curl -s https://codecov.io/bash) -t $CODECOV_TOKEN &&
          echo "Uploaded code coverage"

    test:beta:cargo:
      image: registry.gitlab.com/starshell/docker/rust-codecov:beta
      <<: *cargo_test

    test:nightly:cargo:
      image: registry.gitlab.com/starshell/docker/rust-codecov:nightly
      <<: *cargo_test
