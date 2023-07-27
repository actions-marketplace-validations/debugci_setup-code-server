# Setup Coder code-server

💻 Install [code-server] to run a local VS Code web instance

<div align="center">

![](https://github.com/ttyci/setup-code-server/assets/61068799/8065c44f-2c7c-4925-bb45-b7b788c2d417)

</div>

🌎 Installs `code-server` globally \
👨‍💻 Host your own VS Code web instance to debug CI \
🐧 Works on Linux and macOS runners \
⚠️ Not recommended for extended use \
🚀 No config!

## Usage

![GitHub Actions](https://img.shields.io/static/v1?style=for-the-badge&message=GitHub+Actions&color=2088FF&logo=GitHub+Actions&logoColor=FFFFFF&label=)
![GitHub](https://img.shields.io/static/v1?style=for-the-badge&message=GitHub&color=181717&logo=GitHub&logoColor=FFFFFF&label=)

🛑 You will **not be able to connect** to the `localhost:4000` server unless you
use a tunneling service like [Try Cloudflare] or [ngrok].

This GitHub Action will install the `code-server` binary globally. That means
you can spin up your own local VS Code instance running _on the GitHub Actions
runner_ at any point in your workflow! This is great for diving into a full IDE
(if you need it) to diagnose a problem. For example, debugging the post-build
folder structure and contents of a complex C++ project. Here's a quick demo of
using `code-server` & `cloudflared` to expose a VS Code web instance to the
entire world via [Try Cloudflare].

```yml
on: workflow_dispatch
jobs:
  code-server:
    runs-on: ubuntu-latest
    steps:
      - uses: ttyci/setup-code-server@v1
      - uses: ttyci/setup-cloudflared@v1
      - run: nohup code-server --auth none --bind-addr 0.0.0.0:4000 &
      - run: nohup cloudflared tunnel --url http://localhost:4000 &
      - run: sleep 5m
```

📚 Make sure you check out [the code-server documentation] for a full list of
all the options that you can play around with!

⚠️ Make sure you're aware of [the limits of GitHub Actions]!

### Options

There's currently only a single option to specify the version. Let me know if
there's more options you'd like to see! ❤️

- **`code-server-version`:** The specific pinned version of the `code-server`
  binary to install. This can also be the string `latest` to automatically
  install the latest version. Also supports the `edge` value to install
  prerelease versions. The default is `latest`.

## Development

![GNU Bash](https://img.shields.io/static/v1?style=for-the-badge&message=GNU+Bash&color=4EAA25&logo=GNU+Bash&logoColor=FFFFFF&label=)

This GitHub Action is so simple that we can get away with using plain Bash. To
get started, create a new fork/branch and open a PR! There's some tests in the
`test-action.ym` workflow that will run to make sure everything "works".

<!-- prettier-ignore-start -->
[code-server]: https://github.com/coder/code-server
[the code-server documentation]: https://coder.com/docs/code-server/latest/guide
[try cloudflare]: https://try.cloudflare.com/
[the limits of GitHub Actions]: https://docs.github.com/en/actions/learn-github-actions/usage-limits-billing-and-administration
[ngrok]: https://ngrok.com/
<!-- prettier-ignore-end -->
