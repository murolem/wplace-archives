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

## Archives

### all-map

Contains archives of the entire map. Due to introduction of an RPS limit on wplace, there will likely be no more full archives except those stored.

The archives are structured as per maplibre raster source spec (https://maplibre.org/maplibre-style-spec/sources/#raster): `{x}/{y}.png`

Before they were formatted kind of arbitrary. To reformat an old archive, go to the archive directory after unpacking and run:
<details>
  <summary>Bash</summary>
  
```bash
target_dir="archive_fmted"
target_dirpath="$target_dir"

read -p "Enter the name of an archive folder to process: " archive_source_dir
if [ -d "$archive_source_dir" ]; then
    rm -rf "$target_dir"
    for d in "$archive_source_dir"/*/ ; do
        for f in "$d"/* ; do
            filename="${f##*/}"
            echo "processing: $filename"

            col=${filename:1:4}
            [[ "$col" =~ ^0*(.+)$ ]] && col="${BASH_REMATCH[1]}"
            row=${filename:7:4}
            [[ "$row" =~ ^0*(.+)$ ]] && row="${BASH_REMATCH[1]}"

            mkdir -p "$target_dirpath/$col"
            cp "$f" "$target_dirpath/$col/$row.png"
        done
    done
else
    echo "$archive_source_dir does not exist."
fi
```
</details>
