# uv-cli

> [!TIP]
> As of August 2025 you can use `uv` to [run Python files from the web](https://github.com/astral-sh/uv/pull/15058). Coupled with [script dependencies](https://docs.astral.sh/uv/guides/scripts/#declaring-script-dependencies), you can build powerful gists. But you'll be constrained to single-file applications — module resolution will not work. E.g. run `uv run --python 3.13 https://gist.github.com/seandlg/a9b77f05f02069d9e95db4c5ad691302` to list some Python PEPs. Oh, and please double-check the gist before blindly running it…


Use the following steps to distribute Python applications on *GitHub* using [`uv`](https://docs.astral.sh/uv/).

1. Run `uv init --package` to create a new package.
2. This will create a `pyproject.toml` file with a `[build-system]` section, allowing your package to be built with `uv`.
3. Publish your repository to GitHub (public).

You can now invoke your CLI with the following command:

```bash
uvx --from git+https://github.com/your_username/your_repo_name -- your_package_name
# e.g. uvx --from git+https://github.com/seandlg/uv-cli -- uv-cli --help
```

Note that `uv-cli` is a script under the `[project.scripts]` section of `pyproject.toml`. You can change the name of the script to something else, or add more scripts to the section for other entry points into your package, if needed.

In order to install the CLI as a [`uv` tool](https://docs.astral.sh/uv/guides/tools/), run:

```bash
uv tool install git+https://github.com/your_username/your_repo_name
# e.g. uv tool install git+https://github.com/seandlg/uv-cli
```

This will add simple wrapper scripts for your `[project.scripts]`-commands to `~/.local/bin`, making them available in your shell.

Of course, you could also install these packages to a project:

```bash
uv add git+https://github.com/your_username/your_repo_name
# e.g. uv add git+https://github.com/seandlg/uv-cli
```

This will add the package to your `pyproject.toml` and `uv.lock` files, making it available to your project. If you're building a production package, I recommend sticking with distributing to [`PyPI`](https://pypi.org).

Make sure to cross-reference the awesome [`uv` documentation](https://docs.astral.sh/uv/) for more information.
