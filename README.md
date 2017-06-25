# [DockPress](https://joepurdy.io/words/dockerize-wordpress-with-roots.io)

DockPress is a dockerized version of WordPress inspired heavily by the Roots.io approach to managing a modern WordPress application.

## Features

* Pre-defined development workflow using a single script
* Support for simple initialization of [Bedrock](https://roots.io/bedrock/) and [Sage](https://roots.io/sage/)
* Composer package management
* WP-CLI commands for easier administration

## Requirements

* Docker - [Install](https://www.docker.com/community-edition#/download)

## Installation

1. Run the initialization command with the develop script:

  `./develop init your-theme-name`

2. Update environment variables in `src/.env`  file:
  * `DB_NAME` - Database name
  * `DB_USER` - Database user
  * `DB_PASSWORD` - Database password
  * `DB_HOST` - Database host
  * `WP_ENV` - Set to environment (`development`, `staging`, `production`)
  * `WP_HOME` - Full URL to WordPress home (http://example.dev)
  * `WP_SITEURL` - Full URL to WordPress including subdirectory (http://example.dev/wp)
  * `AUTH_KEY`, `SECURE_AUTH_KEY`, `LOGGED_IN_KEY`, `NONCE_KEY`, `AUTH_SALT`, `SECURE_AUTH_SALT`, `LOGGED_IN_SALT`, `NONCE_SALT`

3. Bring the Docker environment online with `./develop up -d`

4. Create an entry in your hostfile mapping the `WP_HOME` address to `127.0.0.1`

5. Access WP admin at `http://example.dev/wp/wp-admin`

## Contributing

Contributions are welcome from everyone. I don't consider myself an expert here since I only work on WordPress projects once in a blue moon. Check out the [contributing guidelines](https://github.com/joepurdy/DockPress/blob/master/CONTRIBUTING.md) to help you get started.
