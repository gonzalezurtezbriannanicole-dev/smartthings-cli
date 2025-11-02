

## Default Values

When a default value 

## `edgeDriverTestDirs` config option

You can use this option to instruct the CLI to skip files when building an edge driver package. If
you keep your tests in the same directory as your source code (and don't use one of the defaults,
`test` or `tests`, for the base directory of your tests), you should use this to keep them out of
the upload.

You can specify a single string, for example:

```yaml
default:
  edgeDriverTestDirs: specs/**
```

Or, you can specify an array:

```yaml
default:
  edgeDriverTestDirs:
    - specs/**
    - tests/**
```

Files are matched using the `picomatch` library. You find documentation in the
[picomatch README](https://github.com/micromatch/picomatch#basic-globbing) regarding
how to write the matching expressions.

## Example

```yaml
default:
  indent: 4
  groupTableOutputRows: false

tight:
  indent: 1
  groupTableOutputRows: true
```

## On the Command Line

These command line options are hidden from the README and help to reduce clutter since they are
rarely used. (Configuring them via the configuration options above is usually more useful.)
Command line flags always override configuration options.

| option | description |
| -- | -- |
| `--group-rows` | Separate groups of four rows by a line to make long rows easier to follow across the screen. |
| `--no-group-rows` | Do not separate groups of four rows by a line to make long rows easier to follow across the screen. |
| `--indent=<value>` | Indent level for JSON or YAML output. |

## Logging

Logging is useful when you are developing the CLI itself or if you need to debug an issue experienced during general use.

By default, a rolling log file will be created at the [OCLIF CLI cache](https://oclif.io/docs/config) directory.
* macOS: `~/Library/Caches/@smartthings/cli`
* Unix: `~/.cache/@smartthings/cli`
* Windows: `%LOCALAPPDATA%\@smartthings\cli`

The CLI uses [log4js](https://log4js-node.github.io/log4js-node/) for logging.

Logging can be configured using a YAML file called `logging.yaml` in the same
location as the config file mentioned above. The contents of this file are
passed directly to log4js (overriding any default behavior) so any valid log4js configuration can be included
here. The following log categories are used in the CLI:

* `cli` - Generic logger used by the CLI. Log entries will have the command name appended. (ex. `cli.DriversCommand`)
* `rest-client` - Used for the SDK that interfaces with the SmartThings API.
* `login-authenticator` - Used in the default OAuth login flow.
