#`.env` file#
Create a `.env` in the root of Next.js app and add an environment variable for `NEXT_PUBLIC_STRAPI_API_URL`.

> No that `.env` should not be added to the Azure DevOps Git repository. It for local development machines only and can differ from one machine to another.

## Example `.env` file ##
```
NEXT_PUBLIC_STRAPI_API_URL=http://localhost:1337
```