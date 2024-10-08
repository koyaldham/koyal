<h1>Koyal</h1>
[![Ruby Testing](https://github.com/koyaldham/koyal/actions/workflows/test-ruby.yml/badge.svg)](https://github.com/koyaldham/koyal/actions/workflows/test-ruby.yml)

[releases]: https://github.com/koyaldham/koyal/releases
[crowdin]: https://crowdin.com/project/koyaldham

Koyal is a twitter like social platform where users can share cuckoo under moderation of house rules.

Koyal platform is developped on top of Mastodon (stable v4.3.0).

## Deployment

### Tech stack

- **Ruby on Rails** powers the REST API and other web pages
- **React.js** and **Redux** are used for the dynamic parts of the interface
- **Node.js** powers the streaming API

### Requirements

- **PostgreSQL** 12+
- **Redis** 4+
- **Ruby** 3.1+
- **Node.js** 18+

The repository includes deployment configurations for **Docker and docker-compose** as well as specific platforms like **Heroku**, and **Scalingo**. For Helm charts, reference the [mastodon/chart repository](https://github.com/mastodon/chart). The [**standalone** installation guide](https://docs.joinmastodon.org/admin/install/) is available in the documentation.

## Development

### Vagrant

A **Vagrant** configuration is included for development purposes. To use it, complete the following steps:

- Install Vagrant and Virtualbox
- Install the `vagrant-hostsupdater` plugin: `vagrant plugin install vagrant-hostsupdater`
- Run `vagrant up`
- Run `vagrant ssh -c "cd /vagrant && bin/dev"`
- Open `http://mastodon.local` in your browser

### macOS

To set up **macOS** for native development, complete the following steps:

- Install [Homebrew] and run `brew install postgresql@14 redis imagemagick
libidn nvm` to install the required project dependencies
- Use a Ruby version manager to activate the ruby in `.ruby-version` and run
  `nvm use` to activate the node version from `.nvmrc`
- Run the `bin/setup` script, which will install the required ruby gems and node
  packages and prepare the database for local development
- Finally, run the `bin/dev` script which will launch services via `overmind`
  (if installed) or `foreman`

### Docker

For production hosting and deployment with **Docker**, use the `Dockerfile` and
`docker-compose.yml` in the project root directory.

For local development, install and launch [Docker], and run:

```shell
docker compose -f .devcontainer/compose.yaml up -d
docker compose -f .devcontainer/compose.yaml exec app bin/setup
docker compose -f .devcontainer/compose.yaml exec app bin/dev
```

### Dev Containers

Within IDEs that support the [Development Containers] specification, start the
"Mastodon on local machine" container from the editor. The necessary `docker
compose` commands to build and setup the container should run automatically. For
**Visual Studio Code** this requires installing the [Dev Container extension].

### GitHub Codespaces

[GitHub Codespaces] provides a web-based version of VS Code and a cloud hosted
development environment configured with the software needed for this project.

[![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)][codespace]

- Click the button to create a new codespace, and confirm the options
- Wait for the environment to build (takes a few minutes)
- When the editor is ready, run `bin/dev` in the terminal
- Wait for an _Open in Browser_ prompt. This will open Mastodon
- On the _Ports_ tab "stream" setting change _Port visibility_ → _Public_

## Contributing

Mastodon is **free, open-source software** licensed under **AGPLv3**.

You can open issues for bugs you've found or features you think are missing. You can also submit pull requests to this repository or submit translations using Crowdin. To get started, take a look at [CONTRIBUTING.md](CONTRIBUTING.md). If your contributions are accepted into Mastodon, you can request to be paid through [our OpenCollective](https://opencollective.com/mastodon).

**IRC channel**: #mastodon on irc.libera.chat

## License

Copyright (C) 2016-2024 Eugen Rochko & other Mastodon contributors (see [AUTHORS.md](AUTHORS.md))

This program is free software: you can redistribute it and/or modify it under the terms of the GNU Affero General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.

This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU Affero General Public License for more details.

You should have received a copy of the GNU Affero General Public License along with this program. If not, see <https://www.gnu.org/licenses/>.

[codespace]: https://codespaces.new/koyaldham/koyal?quickstart=1&devcontainer_path=.devcontainer%2Fcodespaces%2Fdevcontainer.json
[Dev Container extension]: https://containers.dev/supporting#dev-containers
[Development Containers]: https://containers.dev/supporting
[Docker]: https://docs.docker.com
[GitHub Codespaces]: https://docs.github.com/en/codespaces
[Homebrew]: https://brew.sh
