# anime-offline-database

A single JSON file containing anime from several metadata providers, merged so that every entry
carries the IDs of the same anime on each of them. It answers one question: given an anime on one
site, what is it called on the others.

This repository continues [manami-project/anime-offline-database](https://github.com/manami-project/anime-offline-database),
which was archived on 2026-07-04 with the final release `2026-27`. The dataset here is built by
[modb-app](https://github.com/cedya77/modb-app), a continuation of the original
pipeline, and is seeded from that final release so the merge decisions accumulated upstream are
carried forward rather than rediscovered.

<!-- statistics -->
## Statistics
Update **week 36 [2026]**

The dataset consists of **38137** entries _(76% reviewed)_ composed of:

| Number of entries | Metadata provider |
|-------------------|-------------------|
| 30786 | [myanimelist.net](https://myanimelist.net) |
| 26887 | [anime-planet.com](https://anime-planet.com) |
| 22247 | [kitsu.app](https://kitsu.app) |
| 21105 | [anisearch.com](https://anisearch.com) |
| 20803 | [anilist.co](https://anilist.co) |
| 14621 | [anidb.net](https://anidb.net) |
| 14612 | [simkl.com](https://simkl.com) |
| 14612 | [animecountdown.com](https://animecountdown.com) |
| 12703 | [animenewsnetwork.com](https://animenewsnetwork.com) |
| 12353 | [livechart.me](https://livechart.me) |
<!-- /statistics -->

## Getting the data

The dataset is published as release assets, not as files in this repository. Always fetch from the
`latest` release:

```
https://github.com/cedya77/anime-offline-database/releases/download/latest/anime-offline-database.jsonl
```

| File | Description |
|---|---|
| `anime-offline-database.jsonl` | One anime per line, preceded by a metadata line. Stream it rather than loading it whole. |
| `anime-offline-database-minified.json` | The same data as a single JSON document. |
| `*.zst` | Zstandard compressed variants of both, roughly a tenth of the size. |
| `dead-entries/*.json` | IDs which no longer exist on the respective provider. |

Weekly snapshots are tagged `<year>-<week>`. The `latest` release always points at the most recent
successful run.

## Entry shape

Each entry lists every provider URL it was merged from in `sources`, alongside title, type,
episodes, status, season, tags and related anime. The JSON schemas in [`schemas/`](schemas) are
authoritative, and the dataset validates against them on every release.

```json
{
  "sources": [
    "https://anidb.net/anime/23",
    "https://anilist.co/anime/1",
    "https://myanimelist.net/anime/1"
  ],
  "title": "Cowboy Bebop",
  "type": "TV",
  "episodes": 26,
  "status": "FINISHED"
}
```

An entry with more than one source is a merge that the pipeline is confident about. Entries with a
single source exist on one provider only, or could not be matched with confidence.

## Licence

The dataset is made available under the [Open Database License v1.0](LICENSE) with its contents
under the Database Contents License v1.0, the same terms the original was published under. You are
free to share and adapt it, including commercially, provided you attribute it, keep any redistributed
database under the same licence, and do not use technical measures that restrict others from using it.

Attribution should name both this project and
[manami-project](https://github.com/manami-project), whose work every entry here descends from.

Individual metadata providers hold their own rights over the data they publish. This dataset records
identifiers and the relationships between them.
