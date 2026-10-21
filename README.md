# Swage plugin index

`plugins.json` lists the plugins Swage can install. Swage's **Plugins** page shows every plugin listed here that is not installed yet, and only plugins listed here can be installed or updated.

## Listing a plugin

Add an entry to the `plugins` array:

```json
{
    "name": "swage/gitlab",
    "title": "GitLab",
    "description": "Install repositories from GitLab.com or a self-hosted GitLab, with deploy keys and push-to-deploy webhooks.",
    "kind": "source-control",
    "repository": "https://github.com/Swage-Deploy/swage-plugin-gitlab.git",
    "homepage": "https://github.com/Swage-Deploy/swage-plugin-gitlab"
}
```

| Field | Required | Meaning |
|---|---|---|
| `name` | Yes | The plugin's Composer package name. Swage refuses to install a repository whose `composer.json` has a different name. |
| `title` | No | The name shown on the Plugins page. Defaults to `name`. |
| `description` | No | One or two sentences shown on the Plugins page. |
| `kind` | Yes | What the plugin extends, matching `extra.swage.kind` in its `composer.json`. Only `source-control` exists so far. |
| `repository` | Yes | The git URL Swage installs and updates the plugin from, `https://` for a public repository. |
| `homepage` | No | An `https://` page with more about the plugin, linked from the Plugins page. |

Entries that are missing a required field or have an unknown kind are ignored.

## Review before listing

A plugin runs inside Swage with access to everything it stores, including the SSH keys of every server it manages. Listing a plugin here makes it installable on every Swage that reads this index, and every new version tag it publishes is offered as an update. Only list repositories you trust, and review changes to them.

Swage reads this file from `https://raw.githubusercontent.com/Swage-Deploy/plugin-repo/main/plugins.json`, so this repository must be public. A Swage install can read a different index by setting `SWAGE_PLUGIN_INDEX`.
