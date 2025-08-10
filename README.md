# wplace-archives

Contains archives made with [wplace-archiver](https://github.com/murolem/wplace-archiver).

Compressed on Linux with (creating multipart archive):

```bash
zip -s 100m -r archive.zip <archive_dir>
```

Can be uncompressed on Linux by first creating a single archive:

```bash
zip -F archive.zip --out archive_full.zip
```

Then uncompressing:

```bash
unzip archive_full.zip
```

Windows should be able to open multipart archives as-is.
