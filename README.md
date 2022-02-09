# Digital Garden

> This is a sphinx application for notes related to programming.

## Usage

View this site on [GitHub pages](https://tacoda.github.io/garden/).

## Local

**Dependencies:**

```sh
brew install sphinx-doc
echo 'export PATH="/opt/homebrew/opt/sphinx-doc/bin:$PATH"' >> $HOME/.zshrc
```

**Build html docs:**

```sh
make clean html
```

**Serve the html site:**

```sh
http-server _build/html/
```
