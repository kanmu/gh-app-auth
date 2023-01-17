# gh-app-auth

Authenticate with the GitHub App and generate the installation token.

## Installation

```
$ go install github.com/kanmu/gh-app-auth@latest
```

## Usage

This command will generate and display the installation token based on GitHub App ID, private key and account name.

```
$ gh-app-auth --app-id 12345 --private-key /path/to/private-key.pem --account summerwind
ghs_01234...
```

The flags are used as follows.

```
Usage of gh-app-auth:
  -a, --account string       Target account name
  -i, --app-id int           GitHub App ID
  -h, --help                 Print usage and exit
  -f, --private-key string   Path to the private key file of GitHub App
```

## GitHub Actions

You can run `gh-app-auth` on GitHub Actions to get a installation token as follows.

```yaml
- id: gh-app-auth
  uses: kanmu/gh-app-auth@main
  with:
    app-id: 12345
    private-key: ${{ secrets.GH_APP_AUTH_PRIVATE_KEY }}
    account: summerwind
- run: |
    cat << EOL > ~/.netrc
    machine github.com
    login git
    password ${{ steps.gh-app-auth.outputs.token }}
    EOL
```

## License

MIT license.
