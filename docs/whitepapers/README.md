# Teleflux Whitepapers
Whitepapers of Teleflux system and its subsystems.

## Teleflux
```bash
pandoc --filter pandoc-citeproc -s --toc -V lof teleflux/teleflux_whitepaper.md -o teleflux_whitepaper.pdf --template template.tex --listings -H listings-setup.tex --csl ieee-with-url.csl teleflux/metadata_teleflux.yaml
```

## dFlux
```bash
pandoc --filter pandoc-citeproc -s --toc -V lof dflux/dflux_whitepaper.md -o dflux_whitepaper.pdf --template template.tex --listings -H listings-setup.tex --csl ieee-with-url.csl dflux/metadata_dflux.yaml
```

## dBS
```bash
pandoc --filter pandoc-citeproc -s --toc -V lof dbs/dbs_whitepaper.md -o dbs_whitepaper.pdf --template template.tex --listings -H listings-setup.tex --csl ieee-with-url.csl dbs/metadata_dbs.yaml
```

## dEdge
```bash
pandoc --filter pandoc-citeproc -s --toc -V lof dedge/dedge_whitepaper.md -o dedge_whitepaper.pdf --template template.tex --listings -H listings-setup.tex --csl ieee-with-url.csl dedge/metadata_dedge.yaml
```
