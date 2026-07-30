# How artifacts get here

This repo is the **public artifact registry** for Autobot v3 framework components.
Files here are never edited by hand — they are pushed by CI in the corresponding
private source repos on every tagged release.

## Directory layout

```
manifest.json              ← version index read by Autobot worker
maven-repo/                ← raw Maven repository (served via raw.githubusercontent.com)
  io/vibium/...
python/                    ← Python wheels
npm/                       ← npm tarballs
```

## Adding a new framework

1. Create a private source repo under tribikram1992/.
2. Add a `release.yml` workflow (copy from VibiumFramework/.github/workflows/release.yml).
3. Set secrets: `ARTIFACTS_REPO_TOKEN` (PAT with repo write on THIS repo).
4. On first tag push (`git tag v1.0.0 && git push origin v1.0.0`),
   CI builds the artifact and pushes here automatically.

## Maven repository URL

Generated project pom.xml files use:
```xml
<repository>
  <id>autobot-artifacts</id>
  <url>https://raw.githubusercontent.com/tribikram1992/autobot-framework-artifacts/main/maven-repo</url>
</repository>
```
