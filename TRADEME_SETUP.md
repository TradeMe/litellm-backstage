# TradeMe Setup for LiteLLM Backstage Plugin

This is TradeMe's fork of the LiteLLM Backstage plugin, published to GitLab NPM registry.

## Publishing to GitLab NPM

This repository is mirrored from GitHub to GitLab and automatically publishes to GitLab NPM on git tags.

### Publishing a new version:

1. Update version in `plugins/litellm/package.json`
2. Commit the changes to a branch
3. Create a pull request and merge to main
4. Tag the release:
   ```bash
   git tag v0.2.1
   git push origin v0.2.1
   ```
5. GitLab CI will automatically build and publish to GitLab NPM

### Package Details

- **Package name:** `@trademe/plugin-litellm`
- **Registry:** GitLab NPM (private)
- **GitLab Project:** (Mirror of https://github.com/TradeMe/litellm-backstage)

## Using in tm-backstage

In `tm-backstage` repository:

1. Add to `.npmrc` (or ensure it's configured):
   ```
   @trademe:registry=https://gitlab.com/api/v4/packages/npm/
   //gitlab.com/api/v4/packages/npm/:_authToken=${GITLAB_NPM_TOKEN}
   ```

2. Install the plugin:
   ```bash
   cd src
   yarn add @trademe/plugin-litellm@^0.2.1
   ```

3. Import in `src/packages/app/src/App.tsx`:
   ```typescript
   import { LitellmPage } from '@trademe/plugin-litellm';
   ```

4. Configure in `app-config.production.yaml`:
   ```yaml
   app:
     litellm:
       apiKey: ${LITE_LLM_KEY}
       baseUrl: ${LITE_LLM_URL}
       teamId: ${LITE_LLM_TEAM_ID}
       budgetId: ${LITE_LLM_BUDGET_ID}
       maxBudgetPerUser: ${LITE_LLM_MAX_BUDGET_PER_USER:-999999}
   ```

## Admin Keys for LITE_LLM_KEY Secret

Set these in GCP Secret Manager for each environment:

- **Test:** `sk-oitaFniRtk6kf2ue6a0LTg`
- **Stage:** `sk-mudLQtKEQq1fypwKeD0o5w`
- **Prod:** `sk-iLFVRi5kdURKa5KxmutWZw`

All keys have `proxy_admin` role required for creating users and API keys.
