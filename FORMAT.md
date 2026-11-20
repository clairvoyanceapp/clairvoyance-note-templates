# Default Note Templates

These JSON files are seeded into `config/templates/` in the user data directory
on startup. They define the note templates shown in the sidebar's **New Template**
menu and on the **Templates** dashboard tile.

## Adding a custom template

Drop a JSON file into `config/templates/` (next to the seeded ones). It will be
picked up on the next app launch. Format:

```json
{
  "id": "my-template",
  "name": "My Template",
  "icon": "notebook-pen",
  "noteType": "my-type",
  "order": 100,
  "content": [
    "---",
    "type: my-type",
    "date: {date}",
    "tags: []",
    "---",
    "# My Template — {date}",
    "",
    "## Section",
    ""
  ]
}
```

| Field | Required | Notes |
|-------|----------|-------|
| `id` | yes | Unique identifier. |
| `name` | yes | Display name in menus and on the tile. |
| `content` | yes | Array of markdown lines (or a single string). `{date}`, `{month}`, and `{year}` tokens are replaced at note-creation time. |
| `icon` | no | Icon name from `src/utils/iconResolver.ts` (e.g. `users`, `lightbulb`, `clipboard-check`). Unknown/missing names fall back to a generic icon. |
| `noteType` | no | Frontmatter `type` for notes created from the template. |
| `fileExtension` | no | Defaults to `.md`. |
| `category` | no | Set to `view` to exclude from note-template pickers. |
| `order` | no | Sort key; templates without one sort after ordered ones, by name. |
| `version` | no | Bundled templates only: bumping it refreshes user copies of the same file on upgrade. |

Malformed files are skipped with a console warning — they never break the app.

Editing a **seeded** file works, but a future app version that bumps that
template's `version` will overwrite the bundled-owned fields. Custom files
(your own filenames/ids) are never touched by seeding.
