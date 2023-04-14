# Repos

Repos are listings of compatible packages that creators can use in their projects.

## Format
A repo listing is served in JSON format, with a name, author and listing of packages.

Since each VPM-compatible package has a manifest file with all its info (package.json), we use that in this list. Each manifest is included as the **value** for the [version number](https://semver.org/), under the package name, which is listed as part of a **packages** object.

Here is an example of a repo listing:

```json
{
  "name": "VRChat Official SDK Packages",
  "id": "com.vrchat.official",
  "url": "https://vrchat.github.io/packages/index.json",
  "author": "hello@vrchat.com",
  "packages": {
    "com.vrchat.base": {
      "versions": {
        "3.0.0": {
          "name": "com.vrchat.base",
          "etc": "etc"
        },
        "3.0.1": {
          "name": "com.vrchat.base",
          "etc": "etc"
        }
      }
    },
    "com.vrchat.worlds": {
      "versions": {
        "3.0.0": {
          "name": "com.vrchat.worlds",
          "etc": "etc"
        }
      }
    }
  }
}
```
In the example above, the rest of each version's manifest would be listed, key by key, instead of "etc". To see a live example with full data, take a look at the [Official VRChat Packages repo](https://packages.vrchat.com/official).

Note that you can omit the URL field if you are using a local repo listing file and adding it via the [CLI](/vpm/cli).
