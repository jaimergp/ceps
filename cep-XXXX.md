# CEP XXXX - Declarative, multi-platform file specification for conda environments

<table>
<tr><td> Title </td><td> Declarative, multi-platform file specification for conda environments </td>
<tr><td> Status </td><td> Draft </td></tr>
<tr><td> Author(s) </td><td> Jaime Rodríguez-Guerra &lt;jaime.rogue@gmail.com&gt;</td></tr>
<tr><td> Created </td><td> Jul 4, 2025</td></tr>
<tr><td> Updated </td><td> Jul 4, 2025</td></tr>
<tr><td> Discussion </td><td> NA </td></tr>
<tr><td> Implementation </td><td> NA </td></tr>
</table>

## Abstract

This CEP introduces a new file format, `conda.toml`, to describe multi-platform conda environments for the `conda` CLI tool. It borrows key ideas from the popular `pixi.toml` file format while adjusting it to the unique needs of the established workflows in the classic environment management UX.

## Motivation

Over its long trajectory, the conda ecosystem has accumulated a few file formats to describe the contents of an environment (excluding lockfiles):

- `requirements.txt`, inspired by the user experience in Python packaging tools like `pip`, and standardized in CEP 22.
- `environment.yml`, introduced by `conda env` and standardized in CEP 24, with its multiple variants.
- And more recently, `pixi.toml`, as popularized by Pixi.

The schema complexity has increased in each "generation" to fully capture the metadata that is required to annotate the contents of an environments. From a simple list of package names and versions, we have reached the point where we need several nested dictionaries (or tables, in TOML speech) to explicitly write down all the requirements and their conditions without having to resort to devices like selectors in the form of semantic comments.

This CEP proposes a new standardized file format that takes all the lessons learned in the last years and distilles a number of core features into a simplified TOML document, while carefully enabling `conda` users to describe environments in a single file, impossible with the currently supported formats.

## Specification

https://github.com/jaimergp/conda-declarative/compare/conda-toml-schema

## Rationale

### Why TOML

In the last few years, we have seen a few projects choosing TOML over YAML for their input files: `cargo` uses this to specify Rust projects, the Python community adopted it for `pyproject.toml` and `pylock.toml`, and `tomllib` is now part of the Python standard library since 3.11.

The TOML format has a tighter syntax (e.g. only a few ways to write a string, no anchors, or arbitrary object) that will facilitate simpler ways to achieve the same end result. For example, transitioning from a global key such as `environments` to a nested one such as `tool.conda.environments` only requires a single-line change (the table header), instead of a multiline one to cover the indentation changes.

### Why introduce a new file format instead of adding support for `pixi.toml`?

The full-featured Pixi manifest (`pixi.toml`) is in constant evolution and experiencing a lot of changes as `pixi` matures and adds new capabilities. The feature set `conda` needs is way narrower and we think it will be easier to simply adopt the core ideas introduced by Pixi and adjust them to the needs of the `conda` project.

The full Pixi experience will be there for users that need more from their package management solution, and we believe the similarity between the two formats will bring the two user experiences closer together and allow for a less abrupt transition.

## Backwards compatibility

## Examples

## Acknowled

## References

## Copyright

All CEPs are explicitly [CC0 1.0 Universal](https://creativecommons.org/publicdomain/zero/1.0/).
