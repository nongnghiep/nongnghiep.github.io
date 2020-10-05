# nongnghiep.github.io
name: Font Bakery QA Tests

on: [push, pull_request]

jobs:
  fontbakery:
    runs-on: ubuntu-latest
    name: Font Bakery QA tests  # Customize to edit the string in your GitHub CI UI
    steps:
      - name: Check out source repository
        uses: actions/checkout@v2
      - name: Set up Python environment
        uses: actions/setup-python@v1
        with:
          python-version: "3.8"  # supports any Py3.6+ version available in Actions
      - name: Build fonts
        run: make  # enter your build shell commands here
      - name: fontbakery TTF checks
        uses: f-actions/font-bakery@v1
        with:
          subcmd: "check-universal"  # fontbakery sub-command
          args: "--loglevel WARN"  # optional arguments to fontbakery
          path: "path/to/*.ttf"  # font path relative to root of repository
          version: "latest"  # optional, latest PyPI release is default
      - name: fontbakery OTF checks
        uses: f-actions/font-bakery@v1
        with:
          subcmd: "check-universal"  # fontbakery sub-command
          args: "--loglevel WARN"  # optional arguments to fontbakery
          path: "path/to/*.otf"  # font path relative to root of repository
          version: "latest"  # optional, latest PyPI release is default
