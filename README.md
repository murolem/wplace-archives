# wplace-archives

Contains archives made with [wplace-archiver](https://github.com/murolem/wplace-archiver).

See [releases](https://github.com/murolem/wplace-archives/releases) for all archives. Each archive is named `<type>-<created>`, where `<type>` is a type of an archive (see below) and `<crteated>` is an iso-like datetime of when the archive was created (not including time it took to create it).

# Archives

## World

Tag type: `world`.

Contains archives of the entire map.

The archives are structured as per [Maplibre raster source spec](https://maplibre.org/maplibre-style-spec/sources/#raster), following `{x}/{y}.png` directory structure.

The archives are tar archives compressed with gzip and split into multiple parts, each up to 2Gb in size. Using:

```bash
GZIP=-1 tar czf - "<archive_dir>" | split --bytes=2GB - "<archive_dir>.tar.gz."
```

To unzip, first concatenate all parts back into a single archive by using:

```bash
cat <archive>.tar.gz.* > archive.tar.gz
```

Then, to unzip, use:

```bash
tar -xzf archive.tar.gz
```
