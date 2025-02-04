# Nomad Deploy

This composite GitHub action abstracts away the process of building a Docker
image, pushing it to the ghcr.io registry, and deploying the result to Nomad
according to a given job specification (which defaults to a `nomad.job.hcl`
file in the target repository).

For most use cases, it should be enough to copy the `deploy.example.yml` file
in this repository to `.github/workflows/deploy.yml` in the target repository,
assuming that it already has a `NOMAD_TOKEN` secret set for that repository
(usually, this is done automatically via OpenTofu -- see more information in
the [infra](https://github.com/datasektionen/infra) repository).

The action also assumes that a `NOMAD_ADDR` variable is set at the org level.

When a more complex setup is required, the action strives to be very
configurable (with sensible defaults) and so can often prove sufficiently
extensible to accommodate more esoteric layouts. An example is provided in the
`deploy-dual.example.yml` file in this repository, which shows how one can
build and deploy a single job featuring two separate tasks (frontend and
backend). Slight tweaks may be necessary when using it.
