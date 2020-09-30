# disk-capacity-planner

Calculate filesystem capacity headroom before a maintenance change.

## Run

Python 3.8 or later; no third-party packages or cloud credentials are required.

```sh
python3 tool.py examples/input.json
cat examples/input.json | python3 tool.py -
python3 -m unittest -v
```

## Example

Input:

```json
{
  "total_gib": 100,
  "used_gib": 65,
  "reserve_gib": 10
}
```

Result:

```json
{
  "available_gib": 35.0,
  "usable_headroom_gib": 25.0,
  "used_percent": 65.0
}
```

The command writes JSON to standard output. Exit 0 means evaluation completed;
a finding in the output may still require attention. Invalid input returns exit 2,
with an error on standard error and no result on standard output.

## Operational scope

Uses a static snapshot; filesystem reserved blocks and growth rates are not collected.

The tool evaluates supplied data locally. It does not change hosts, deploy
resources, or establish production compliance. Example identifiers and observations
are test fixtures. Keep credentials and private inventory out of Git.

## Design and verification

See [NOTES.md](NOTES.md) for the input contract, verification, and integration notes.
Related utilities: [log-level-counter](https://github.com/sal-s-root/log-level-counter), [inode-usage-checker](https://github.com/sal-s-root/inode-usage-checker).
