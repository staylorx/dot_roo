# CLI

If the app has a CLI, and most of my domain and data core packages do, I've copied out this for your reference:

The CLI in this project uses the standard **subcommand pattern** that's widely adopted across modern command-line tools. Here's the structure:

```
main [global-flags] <command> [command-flags] [args]
```

**Examples from the codebase:**

- `main --verbose deck list`
- `main --db-path ./custom deck import my_deck.apkg`
- `main config set current-deck my-deck`

**Key characteristics:**

- **Global flags** come first (like `--verbose`, `--db-path`, `--config-path`)
- **Subcommand** follows (like `deck`, `config`, `session`, `status`)
- **Command-specific flags** come after the subcommand (like `--format`, `--algorithm` for deck commands)
- **Arguments** come last

This is the same pattern used by:

- **kubectl** (Kubernetes CLI)
- **docker**
- **git** (though git has some variations)
- **GitHub CLI (gh)**
- **AWS CLI**
- And many others

**Is there a standard?** While there's no formal specification from a single organization, this hierarchical subcommand pattern has become the de facto standard for complex CLIs. It's recommended by CLI design best practices and toolkits like:

- [Command Line Interface Guidelines](https://clig.dev/) (unofficial but widely referenced)
- [12 Factor CLI Apps](https://medium.com/@jdxcode/12-factor-cli-apps-dd3c227a0e46)
- Dart's `args` package documentation

The pattern provides clear separation of concerns, discoverability through `--help`, and scales well as applications grow. Your implementation follows this standard perfectly.
