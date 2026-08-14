# OpenVSD Workshop

This repository hosts the community plugin listing for **OpenVSD**. The app fetches [`workshop.yml`](./workshop.yml) directly from this repo to populate the in-app Workshop, so adding your plugin here makes it discoverable and installable by every OpenVSD user.

## How it works

`workshop.yml` is a YAML list of plugin entries. Each entry describes one plugin: its name, a short description, and a URL the app can download it from. When a user opens the Workshop panel in OpenVSD, this file is parsed and turned into the list they browse and install from.

## Adding your plugin

1. **Fork this repository.**

2. **Generate a unique ID** for your plugin. This is a GUID that will identify your entry permanently — don't reuse or change it later. You can generate one with:
   - PowerShell: `[System.Guid]::NewGuid()`
   - Linux: `uuidgen`
   - Or any online GUID generator

3. **Add an entry to `workshop.yml`.** Open the file and append a new list item following this format:

   ```yaml
   - ID: 3fa85f64-5717-4562-b3fc-2c963f66afa6
     Name: Your Plugin Name
     Description: A short, clear sentence describing what your plugin does.
     GithubUrl: https://github.com/yourname/your-plugin/releases/latest/download/YourPlugin.dll
   ```

4. **Open a pull request** from your fork back to this repo, with only your addition to `workshop.yml` in the diff.

That's it — once merged, your plugin will appear in the Workshop for all users the next time they refresh the listing.

## Field reference

| Field | Required | Notes |
|---|---|---|
| `ID` | Yes | A GUID, unique across the whole file. Generate once and never change it — it's how the app looks up and tracks your plugin across updates. |
| `Name` | Yes | Display name. Also used to match against installed DLLs, so keep it consistent with your plugin's actual file name (without the `.dll` extension). |
| `Description` | Yes | One or two sentences. Shown in the Workshop UI, so keep it concise. |
| `GithubUrl` | Yes | A direct, public download link — see below. |

## Requirements for `GithubUrl`

This URL must resolve directly to file bytes, not an HTML page. It's fetched as either:

- **A single `.dll`** — the app saves it directly into the plugin folder as `<Name>.dll`.
- **A `.zip` archive** — the app extracts every file inside it into the plugin folder. Use this if your plugin ships with dependencies or multiple DLLs.

**Use one of these link types:**

- A GitHub **release asset** URL, e.g.:
  `https://github.com/yourname/your-plugin/releases/latest/download/YourPlugin.dll`
- A `raw.githubusercontent.com` URL to a committed file

**Do not use:**

- A `github.com/.../blob/...` link — this returns an HTML page, not the raw file, and will fail to install.
- Links behind authentication, redirects that require a browser, or hosts that block automated requests.

We recommend using [GitHub Releases](https://docs.github.com/en/repositories/releasing-projects-on-github/managing-releases-in-a-repository) in your own plugin repo and pointing `GithubUrl` at the `latest` release asset, so updating your plugin's binary doesn't require a PR here — only changing the entry itself (e.g. name or description) does.

## Before you submit

- [ ] `ID` is a freshly generated GUID not already used elsewhere in the file
- [ ] `Name` matches the filename your plugin DLL will install as
- [ ] `GithubUrl` points directly to a `.dll` or `.zip`, and you've tested that the link downloads correctly with no login/redirect
- [ ] YAML is valid — list items are indented consistently and use `-` at the same level as other entries
- [ ] Your addition is the only change in the PR diff

## Removing or updating an entry

Open a pull request editing or removing your existing entry. Please keep the same `ID` if you're updating an existing plugin rather than replacing it — this avoids orphaning any state tied to the old ID.

## Questions or issues

If you run into trouble formatting your entry or your plugin isn't loading correctly after being added, open an issue in this repo and we'll help sort it out.
