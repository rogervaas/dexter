# Dexter

An automatic indexer for Postgres

## Installation

First, install [HypoPG](https://github.com/dalibo/hypopg) on your database server. This doesn’t require a restart.

```sh
wget https://github.com/dalibo/hypopg/archive/1.0.0.tar.gz
tar xf 1.0.0.tar.gz
cd hypopg-1.0.0
make
make install
```

> Note: If you have issues, make sure `postgresql-server-dev-*` is installed.

Enable logging for slow queries.

```ini
log_min_duration_statement = 10 # ms
```

And install with:

```sh
gem install pgdexter
```

## How to Use

Dexter needs a connection to your database and a log file to process.

```sh
tail -F -n +1 <log-file> | dexter <database-url>
```

This finds slow queries and generates output like:

```log
2017-06-25T17:52:19+00:00 Started
2017-06-25T17:52:22+00:00 Processing 189 new query fingerprints
2017-06-25T17:52:22+00:00 Index found: genres_movies (genre_id)
2017-06-25T17:52:22+00:00 Index found: genres_movies (movie_id)
2017-06-25T17:52:22+00:00 Index found: movies (title)
2017-06-25T17:52:22+00:00 Index found: ratings (movie_id)
2017-06-25T17:52:22+00:00 Index found: ratings (rating)
2017-06-25T17:52:22+00:00 Index found: ratings (user_id)
2017-06-25T17:53:22+00:00 Processing 12 new query fingerprints
```

To be safe, Dexter will not create indexes unless you pass the `--create` flag.

## Options

- `--interval` - time to wait between processing queries, in seconds (default: 60)
- `--min-time` - only consider queries that have consumed a certain amount of DB time, in minutes (default: 0)

## Contributing

Everyone is encouraged to help improve this project. Here are a few ways you can help:

- [Report bugs](https://github.com/ankane/dexter/issues)
- Fix bugs and [submit pull requests](https://github.com/ankane/dexter/pulls)
- Write, clarify, or fix documentation
- Suggest or add new features
