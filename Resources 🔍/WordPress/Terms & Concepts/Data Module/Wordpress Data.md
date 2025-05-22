WordPress’ data module serves as a hub to manage application state for both plugins and WordPress itself, providing tools to manage data within and between distinct modules. It is designed as a modular pattern for organizing and sharing data: simple enough to satisfy the needs of a small plugin, while scalable to serve the requirements of a complex single-page application.

The data module is built upon and shares many of the same core principles of [Redux](https://redux.js.org/), but shouldn’t be mistaken as merely _Redux for WordPress_, as it includes a few of its own [distinguishing characteristics](https://developer.wordpress.org/block-editor/reference-guides/packages/packages-data/#comparison-with-redux). As you read through this guide, you may find it useful to reference the Redux documentation — particularly [its glossary](https://redux.js.org/glossary) — for more detail on core concepts.

## Resource
- [Package Reference - @wordpress/data](https://developer.wordpress.org/block-editor/reference-guides/packages/packages-data/)
