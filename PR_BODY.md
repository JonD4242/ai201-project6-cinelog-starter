PR: Watchlist Feature — Project 5 Submission

Summary

This PR implements the watchlist feature and addresses all graded feedback comments. Key changes:

- Renamed `save_to_watchlist()` to `add_to_watchlist()` to match the project's naming convention.
- Added deduplication logic and `AlreadyInWatchlistError` to prevent duplicate watchlist entries.
- Implemented tests in `tests/test_watchlist.py` for nonexistent film and duplicate entry.
- Restored and adapted the `WatchlistEntry` model to use UUID `film_id` to match `Film.id`.
- `WatchlistEntry.public` defaults to `True` (public-by-default behavior documented).
- `get_watchlist()` returns entries newest-first (sorted by `date_added` descending).
- Added `pr-response.md` documenting how each reviewer comment was addressed.

Verification

- Ran unit tests: `pytest` — all tests passed (7 passed).

How to review

1. View the branch: https://github.com/JonD4242/ai201-project5-mixtape-starter/tree/project5
2. Compare to upstream: https://github.com/jamjamgobambam/ai201-project5-mixtape-starter/compare/main...JonD4242:project5?expand=1
3. Running tests locally:

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
pytest
```

Notes

If you want me to open the PR for you, I can create the PR title/body on GitHub (requires using your account or an auth token). Otherwise the links above let you submit from the browser. 
