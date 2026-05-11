# testwindowtree

Python client for Treeland's `WindowTreeRemote` Qt Remote Object.

The client is built from the static Replica generated from
`src/treeland_windowtree.rep`; it does not use `QRemoteObjectDynamicReplica`.

## Build

```bash
uv sync
```

`uv` installs the Python build requirements. The native extension also needs the
system Qt6 Remote Objects development tools:

- `pkg-config`
- Qt6 Core and RemoteObjects development files
- `repc` and `moc` from Qt6

The build defaults to `/usr/lib/qt6/libexec/repc` and
`/usr/lib/qt6/libexec/moc`. Override with `REPC=/path/to/repc` or
`MOC=/path/to/moc` if needed.

## Usage

```python
from treeland_windowtree import WindowTreeClient

client = WindowTreeClient()
layers = client.get_full_layout_tree()
cursor = client.cursor_position()
```

CLI:

```bash
uv run testwindowtree
uv run testwindowtree --cursor
```

Default connection values match Treeland:

- URL: `local:treeland.windowtree`
- Replica name: `WindowTree`

The returned tree is converted to Python dictionaries/lists, including nested
`QList<LayerInfo>`, `QList<WorkspaceInfo>`, and `QList<WindowInfo>` values.
