# Maintaining the Quantum Notebook

The detailed add-a-deck checklist, stable-path rules, citation conventions and size budgets are in [agent/NOTES.md](../agent/NOTES.md). Coding assistants should also read [CLAUDE.md](../CLAUDE.md).

The public archive contains PDFs, curated metadata, thumbnails, and a static website. Keep published item IDs and BibTeX keys stable so citations continue to resolve.

## Add or update a deck

```sh
python3 tools/add_deck.py NEW.pdf --shelf research --title "Title" --year 2027 --venue "Venue"
```

Use `research`, `lectures`, or `notes` as appropriate (see `python3 tools/add_deck.py --help` for supported choices). Confirm title, date, venue, authors, summary, and links against the source deck. Curated metadata belongs in `tools/catalog_overrides.json`; regenerate `catalog.json` rather than editing generated records.

```sh
python3 tools/build_catalog.py
python3 tools/make_thumbnails.py
python3 tools/check_sizes.py
python3 tools/build_site.py
```

PDF processing requires Ghostscript; thumbnail generation requires the tools imported by `tools/make_thumbnails.py`. Use `--with-pdfs` when building a self-contained local website with copied PDFs. Default builds link to hosted PDFs. Run `python3 tools/build_site.py --serve` to preview on port 8000.

## Citations and releases

Commit updated metadata, thumbnails, and frozen citation keys with source changes. Keep large PDFs compressed; check size budgets before publishing. Deployment is configured in `.github/workflows/site.yml`. Coordinate URL changes with citation metadata and redirects before deploying.

`tools/zenodo_deposit.py` supports DOI deposits. Review its help and the prepared records before publishing them; final DOI publication is permanent. Use stable public URLs for deposited materials.
