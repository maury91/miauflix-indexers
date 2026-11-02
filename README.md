# Miauflix indexers

Extra indexer definitions for [Miauflix](https://github.com/maury91/miauflix), in the
[Cardigann YAML format](https://wiki.servarr.com/en/prowlarr/cardigann-yml-definition) used by
Prowlarr and Jackett.

Miauflix contains no indexer-specific code: it reads definitions from the folders listed in its
`CARDIGANN_DEFINITION_SOURCES` setting and runs them with its own engine. By default that is
[Prowlarr's definitions](https://github.com/Prowlarr/Indexers/tree/master/definitions/v11) and the
`definitions` folder of this repository:

```
https://github.com/maury91/miauflix-indexers/tree/main/definitions
```

This repository only holds definitions that are missing from, or do not search by IMDb id in,
those collections. Each file is a description of how to query a public website's own JSON; none of
them contains any content.

| Definition | What it adds |
| --- | --- |
| `eztv-api.yml` | TV episodes by IMDb id through EZTV's JSON API (`/api/get-torrents`), 100 per page. EZTV's definition in Prowlarr and Jackett only searches by title. |
| `therarbg-imdb.yml` | The newest releases of one IMDb title through TheRARBG's per-title page. Prowlarr no longer ships TheRARBG, and the IMDb search in Jackett's definition no longer works. |

Use another folder, or any other repository, by adding its URL to `CARDIGANN_DEFINITION_SOURCES`
(space or comma separated): a GitHub folder as `https://github.com/<owner>/<repo>/tree/<branch>/<path>`,
or any web folder that serves an `index.json` listing its definition ids.

## Contributing

A definition is one `.yml` file in `definitions/`, named after its `id`. It should:

- be `type: public`, so no account or login is needed;
- declare only the search parameters the site really supports in `caps.modes`;
- search by IMDb id (`imdbid`) where the site allows it.

Miauflix supports the subset of the format that its engine implements; a definition that uses
anything else is listed as unsupported rather than failing.

## License

[MIT](LICENSE)
