# Rev Obsidian Sync

Reverse engineered obsidian sync server (NOT OFFICIAL).

> [!WARNING]
> The main branch is the development branch. For stable usage, use the latest release.

> [!NOTE]
> The plugin is broken on `obsidian >= 1.4.11`. This is intentional by the official ObsidianMD team. They have made clear their dissatisfaction with this project.
> [The Path Forward](https://github.com/acheong08/obi-sync/issues/29) - We are in the early stages of designing an alternative plugin that does not make use of existing code by ObsidianMD team. It is still in the design phase and [help](https://github.com/acheong08/obi-sync-lib/issues/1) is needed. DO NOT UPGRADE

## Features

- End to end encryption
- Live sync (across devices)
- File history/recovery/snapshots
- Works natively on IOS/Android/Linux/MacOS/Windows... (via the plugin)
- Vault sharing
- [Publish (markdown only. no rendering yet)](https://github.com/acheong08/obi-sync/wiki/Obsidian-Publish)

### Experimental

These features are not in the latest release but in the main branch. They might not be fully tested and are probably unstable.

- N/A

## To do

- Fix bugs
- Improve publish

## Quickstart

> [!NOTE]
> The comprehensive documentation by @Aetherinox can be found in the [wiki](https://github.com/acheong08/obi-sync/wiki).


[Quickstart with Docker](https://github.com/acheong08/rev-obsidian-sync/blob/main/docker-compose.yml)

### Environment variables

#### Required:

- `DOMAIN_NAME` - The domain name or IP address of your server. Include port if not on 80 or 433. The default is `localhost:3000`

#### Optional

- `ADDR_HTTP` - Server listener address. The default is `127.0.0.1:3000`
- `SIGNUP_KEY` - Signup API is at `/user/signup`. This optionally restricts users who can sign up.
- `DATA_DIR` - Where data is saved. Default `.`
- `MAX_STORAGE_GB` - The maximum storage per user in GB. Default `10`
- `MAX_SITES_PER_USER` - The maximum number of sites per user. Default `5`

### Building & Running

- `git clone https://github.com/acheong08/obsidian-sync`
- `cd obsidian-sync`
- `go run cmd/obsidian-sync/main.go`

Optional:

- Configure [nginx](https://github.com/acheong08/rev-obsidian-sync/wiki/Nginx-Configuration)
- HTTPS is recommended.

When you're done, install and configure the [plugin](https://github.com/acheong08/rev-obsidian-sync-plugin)

## Adding a new user

`go run cmd/signup/main.go`

Alternatively:

```bash
curl --request POST \
  --url https://yourdomain.com/user/signup \
  --header 'Content-Type: application/json' \
  --data '{
	"email": "example@example.com",
	"password": "example_password",
	"name": "Example User",
	"signup_key": "<SIGNUP_KEY>"
}'
```

You can set the signup key via the `SIGNUP_KEY` environment variable. If it has not been set, you can exclude it from the request.
