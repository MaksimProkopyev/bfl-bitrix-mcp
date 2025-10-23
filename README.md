# bfl-bitrix-mcp

Init commit.

## Local development

1. Install Node.js 20 (the repo includes an `.nvmrc` file if you use `nvm`).
2. Run schema validation locally:

   ```bash
   npm run validate:schemas
   ```

   The command downloads `ajv-cli@5` and `ajv-formats` on demand to ensure the
   JSON schemas in `schemas/` compile successfully.
