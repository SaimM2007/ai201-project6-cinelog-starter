# PR Response Doc — CineLog Watchlist Feature

## AI Usage
<!-- Fill in at the end — how you used AI tools during this project -->

## Comment 1 — Rename
**What I did:** Renamed save_to_watchlist() to add_to_watchlist() in services/watchlist_service.py so it matches the verb_to_noun naming that add_to_collection() already uses. Also updated the one place it was called from, routes/watchlist/watchlist.py, both the import and the actual call.
**How I verified:** Searched the whole repo for save_to_watchlist to make sure nothing still referenced the old name (used Select String since I'm on PowerShell, not grep). Came back empty. Ran the test suite after too just to be safe.

## Comment 2 — Deduplication
**What I did:** Added an AlreadyInWatchlistError exception and a check for an existing entry before creating a new one in add_to_watchlist(). Basically copied the same approach add_to_collection() uses in collection_service.py, look up the film, look up if the entry already exists, and if it does, raise the error instead of just letting a duplicate get created.
**How I verified:** Ran the full test suite after making the change and everything still passed. I didn't write a dedicated duplicate test for this one since it wasn't explicitly asked for in Comment 3, but I could add one later if I have time (would be a good stretch test).

## Comment 3 — Missing test
**What I did:** Made a new file, tests/test_watchlist.py, and wrote test_add_to_watchlist_nonexistent_film_raises. Basically copied the structure of test_add_to_collection_nonexistent_film_raises from test_collection.py, same fixtures, same idea of checking that a fake film id raises FilmNotFoundError. One thing I changed: I used a fake integer (999999) instead of a fake UUID string, since Film.id is still an integer on this branch until the rebase happens in Comment 6. Will need to update this once that lands.
**How I verified:** Ran pytest tests/test_watchlist.py -v and it passed. Then ran the whole suite with pytest tests/ -v and all 5 passed.

## Comment 4 — Default visibility
**My position:**
**Reasoning:**
**Tradeoff acknowledged:**

## Comment 5 — Sort order
**My position:**
**Reasoning:**
**Engagement with reviewer's point:**

## Comment 6 — Rebase
**What conflicted:**
**How I resolved it:**
**How I verified no conflict remains:**

## PR Description
<!-- Written at the end — feature overview, design decisions, manual testing steps -->