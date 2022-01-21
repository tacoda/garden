# Destroy All Software

> This is a sphinx application for notes related to programming.

## Usage

Goal: CI via GitHub action for pdf, html, epub. (and maybe others)

## Developing

**Dependencies:**

```sh
brew install sphinx-doc
echo 'export PATH="/opt/homebrew/opt/sphinx-doc/bin:$PATH"' >> $HOME/.zshrc
```

**Build html docs:**

```sh
make html
```

**Serve the html site:**

```sh
http-server _build/html/
```
