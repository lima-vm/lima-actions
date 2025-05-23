# Lima on GitHub Actions

[Lima](https://lima-vm.io) is useful for running non-Ubuntu distributions such as Fedora on GitHub Actions.

## Usage

```yaml
steps:
  - uses: actions/checkout@v4

  - uses: lima-vm/lima-actions/setup@v1
    id: lima-actions-setup

  - uses: actions/cache@v4
    with:
      path: ~/.cache/lima
      key: lima-${{ steps.lima-actions-setup.outputs.version }}

  - run: limactl start --plain --name=default --cpus=1 --memory=1 template://fedora

  - uses: lima-vm/lima-actions/ssh@v1

  - run: rsync -a -e ssh . lima-default:/tmp/repo

  - run: ssh lima-default ls -l /tmp/repo
```

## Optional parameters
### `lima-vm/lima-actions/setup`
- `version` (string): Lima version. e.g., "latest", "v1.0.6". Defaults to "latest".
- `additional_guestagents` (boolean): Install lima-additional-guestagents. Usually not needed. Defaults to `false`.

### `lima-vm/lima-actions/ssh`
None
