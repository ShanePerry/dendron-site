---
id: 26be950a-eaf3-4684-bddd-64be52273b73
title: Schema
desc: ''
updated: 1608527506447
created: 1608527496774
---
```
  "root": Object {
    "fname": "root",
    "imports": Array [],
    "root": Object {
      "children": Array [],
      "id": "root",
      "parent": "root",
      "title": "root",
    },
    "schemas": Object {
      "root": Object {
        "body": "",
        "children": Array [],
        "created": 1605108880847,
        "data": Object {},
        "desc": "",
        "fname": "__empty",
        "id": "root",
        "links": Array [],
        "parent": "root",
        "title": "root",
        "type": "schema",
        "updated": 1605108880847,
        "vault": undefined,
      },
    },
    "version": 1,
  },
```

# Renaming a Note

## Flow

- engine-server/src/drivers/file/storev2.ts

```ts
renameNote opts {
  oldNote, oldLoc, newLoc := opts
  notesToChange = getNotesWithLinkTo(oldNote)
  notesToChange.forEach { n =>
    replaceLinks(n, from: oldLoc, to: newLoc)
    n.links = findLinks(n)
  }
  newNote = {oldNote, newLoc}
  @deleteNote( oldNode, metaOnly)
}
```

- src/topics/markdown/utilsv2.ts

```ts
replaceLinks opts {
  remark = getRemark(dendronLinksOpts: {replaceLink: { from, to }} )
  return remark.process(opts.content).toString()
}
```

- src/drivers/file/storev2.ts

```ts
deleteNote(note) {
  ...
  if !note.children {
    ...
  } else {
  }

}

```

- See [[Remark|dendron.dev.design.remark]]

# Specifics

### Does Dendron use parent/children metadata inside notes during initialization?

- src/filesv2.ts: `string2Note`

# WorkspaceService: Add Vault

- src/workspace.ts

```ts
createVault(vault, noAddToConfig):
  ensureDir(vault)
  createNoteRoot if not_exist
  createSchemaRoot if not_exist

  if !noAddToConfig:
    config.add vault
```

