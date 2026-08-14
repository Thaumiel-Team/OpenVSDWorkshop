## Type of change

- [ ] Adding a new plugin
- [ ] Updating an existing plugin entry
- [ ] Removing a plugin

## Checklist

- [ ] My change only modifies `workshop.yml` (no unrelated files changed)
- [ ] `ID` is a valid GUID
  - [ ] **New plugin:** freshly generated, not reused from another entry
  - [ ] **Update/removal:** unchanged from the existing entry
- [ ] `Name` matches the filename my plugin installs as (without the `.dll` extension)
- [ ] `Description` is a short, accurate summary (one or two sentences)
- [ ] `GithubUrl` points directly to a `.dll` or `.zip` file
  - [ ] Not a `github.com/.../blob/...` page link
  - [ ] I tested the link downloads the file directly, with no login or redirect
- [ ] YAML is valid — list items are indented consistently and use `-` at the same level as other entries
- [ ] I've read [`README.md`](../README.md) for full field requirements

## Plugin details

**Name:**

**Description:**

**Repo / source link:**

## Notes for reviewers

<!-- Anything reviewers should know: first-time submission, breaking changes to an existing entry, etc. -->
