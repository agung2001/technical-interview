WP Stash is a bridge between StashPHP and WP's object caching drop-in support. It enables APCu, Redis, SQLite, Memcached, and Filesystem caches, stampede protection, and group invalidation.

After installing, it will copy an `object-cache.php` file to `wp-content/` which will delegate all cache calls to its mu-plugin folder. From there, it will interface with StashPHP.

## Resource
- [Github - inpsyde/WP-Stash](https://github.com/inpsyde/WP-Stash)