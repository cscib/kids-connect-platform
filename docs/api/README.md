# Maltese Quest API Documentation

The interactive API documentation is generated automatically from `openapi.yaml`
and published to GitHub Pages on every push to `main`.

## View docs

Once GitHub Pages is enabled, your docs will be live at:

```
https://<your-github-username>.github.io/<your-repo-name>/
```

## Preview locally

```bash
npx @redocly/cli preview-docs docs/api/openapi.yaml
```

## Validate the spec locally

```bash
npx @redocly/cli lint docs/api/openapi.yaml
```

## Rebuild static HTML locally

```bash
npx @redocly/cli build-docs docs/api/openapi.yaml --output docs/api/index.html
```
