# Anodosys registry

The public registry of [Anodosys](https://github.com/anodosys/app) extensions. `ads extension install <name>` looks up the name here and installs the newest matching version with its dependencies:

```bash
ads extension install cosyses
ads extension install cosyses@^1.0
ads extension search
```

## Format

`registry.json` maps every extension name to its git repository:

```json
{
  "extensions": {
    "cosyses": {
      "url": "https://github.com/cosyses/anodosys.git",
      "description": "Cosyses base images with Cosyses preinstalled"
    }
  }
}
```

The value can also be just the url. The versions of an extension are the semver tags of its repository (`1.2.3`), so a new version needs no change here. Its `extension.json` names it and lists what it requires:

```json
{
  "name": "magento",
  "description": "Magento systems and images",
  "anodosys": ">=4.0",
  "requires": { "fewedev": "^1.0" },
  "sources": { "fewedev": "git@github.com:fewe-dev/anodosys.git" }
}
```

`sources` tells where to find a required extension that no registry knows, for example a private one.

## Adding an extension

Open a pull request that adds the extension to `registry.json`. The repository must be public and have at least one version tag and an `extension.json`.

## Private extensions

Private extensions do not belong here. Put them into a registry of your own, a git repository (reachable with your git login, for example over SSH) or a local directory with the same `registry.json`, and add it on every machine:

```bash
ads extension registry add git@github.com:company/anodosys-registry.git
```

Registries added this way are searched before this one, so they can also replace a public extension. Without a registry, `ads extension install owner/repo` installs a GitHub repository directly (https, then ssh), and `ads extension install <git url>` any other.
