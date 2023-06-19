#`.env` file#
Create a `.env` in the root of Next.js app and add environment variables for `NEXT_PUBLIC_STRAPI_API_URL` and `NEXT_PUBLIC_STRAPI_API_TOKEN`.

> Note that `.env` should not be added to the Azure DevOps Git repository. It is for local development machines only and can differ from one machine to another.

## Example `.env` file ##
```
NEXT_PUBLIC_STRAPI_API_URL=http://localhost:3036
NEXT_PUBLIC_STRAPI_API_TOKEN=<secret API token>
```