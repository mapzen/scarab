# 3.1.0

- Added `description` support. If a `description` string is provided in options, an info button appears. Clicking on it will display a box showing `description` as its contents. Clicking on the button again toggles it off.
- The `repo` option no longer has a default repository URL. If not provided, the GitHub button will not appear.
- Scarab centering is now based on the contents of the scarab and will dynamically position itself. It is no longer controlled via CSS. If you have any CSS that overrides vertical centering you will need to update this.

# 3.0.0

- scarab standalone build extracted from former mapzen-ui bundle.
