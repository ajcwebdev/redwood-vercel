# Redwood+Vercel ▲

> **NOTICE:** RedwoodJS is very close to a stable version 1.0. In the last two years,
> the project has matured significantly and is already used in production by a number
> of startups. We intend to have a 1.0 release candidate before the end of 2021 and
> to release a truly production-ready 1.0 in early 2022.

## Getting Started

- [Tutorial](https://redwoodjs.com/tutorial/welcome-to-redwood): getting started and complete overview guide.
- [Docs](https://redwoodjs.com/docs/introduction): using the Redwood Router, handling assets and files, list of command-line tools, and more.
- [Redwood Community](https://community.redwoodjs.com): get help, share tips and tricks, and collaborate on everything about RedwoodJS.

### Setup

We use Yarn as our package manager. To get the dependencies installed, just do this in the root directory:

```terminal
yarn install
```

### Fire it up

```terminal
yarn redwood dev
```

Your browser should open automatically to `http://localhost:8910` to see the web app. Lambda functions run on `http://localhost:8911` and are also proxied to `http://localhost:8910/api/*`.

### Vercel Configuration

This example used the [`yarn rw setup deploy vercel`](https://redwoodjs.com/docs/deploy#vercel-deploy) command to modify `redwood.toml`, the default Redwood configuration like so:

```diff
[web]
  title = "Redwood App"
  port = 8910
- apiUrl = "/.redwood/functions"
+ apiUrl = "/api"
  includeEnvironmentVariables = []
[api]
  port = 8911
[browser]
  open = true
```

After running the setup command, the [`apiUrl`](https://redwoodjs.com/docs/app-configuration-redwood-toml#web) is changed from `/.redwood/functions` to `/api`.

### Test Deployed API

Test the endpoint with `curl`:

```bash
curl \
  --request POST \
  --header 'content-type: application/json' \
  --url 'https://redwood-vercel.vercel.app/api/graphql' \
  --data '{"query":"{ redwood { version } }"}'
```

This will return the following output:

```json
{
  "data":{
    "redwood":{
      "version":"0.43.0"
    }
  }
}
```
