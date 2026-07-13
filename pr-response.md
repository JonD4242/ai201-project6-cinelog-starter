# PR Response Doc — CineLog Watchlist Feature

## AI Usage
<!-- Fill in at the end -->

## Comment 1 — Rename
**What I did:** I renamed `save_to_watchlist()` to `add_to_watchlist()` in `services/watchlist_service.py` to match the project’s `verb_to_noun` naming convention used by `add_to_collection()`, and I updated the related import and call site in `routes/watchlist/watchlist.py`.
**How I verified:** I ran a project-wide search for `save_to_watchlist` and confirmed that all 3 occurrences across 2 files had been updated. I also ran `pytest tests/ -v`, and the existing test suite still passed.

## Comment 2 — Deduplication
**What I did:** I added a watchlist-specific duplicate check in `services/watchlist_service.py` so adding the same film twice now raises `AlreadyInWatchlistError` before a second entry is created.
**How I verified:** I verified this through the new test `test_add_to_watchlist_duplicate_raises`, which confirms that a second add raises `AlreadyInWatchlistError` and that only one entry remains in the database.

## Comment 3 — Missing test
**What I did:** I created `tests/test_watchlist.py` with a nonexistent-film test modeled on the collection test pattern and a duplicate-entry test to cover the new deduplication behavior.
**How I verified:** I ran `pytest tests/ -v` in the project virtual environment, and all 6 tests passed.

## Comment 4 — Default visibility
**My position:** Public-by-default is the right default for watchlists in CineLog.
**Reasoning:** In CineLog, a watchlist is more than a private record of past viewing; it is a signal of what a user is interested in and wants to explore next. Because the app is built around community-driven film discovery, that kind of interest data can support recommendations, social connection, and serendipitous discovery. A public watchlist makes it easier for others to find people with similar tastes, follow emerging interests, and discover films they might not otherwise encounter. I also think this information feels less sensitive than a completed collection because it reflects intent rather than a finished record of consumption, so making it visible by default fits the app’s social purpose.
**Tradeoff acknowledged:** The tradeoff is that public-by-default exposes a user’s interests and intentions more openly than a privacy-first approach would. Some users may not want their current viewing goals or niche tastes visible by default, especially while they are still exploring or experimenting. I am choosing the more social and discoverable behavior, even though it gives up some privacy and may require users to opt out if they want a more private experience.

## Comment 5 — Sort order
**My position:** I agree with the reviewer that the watchlist should be ordered by recency rather than alphabetically.
**Reasoning:** A watchlist is a live queue of films a user wants to engage with next, so the most relevant items are usually the ones they added most recently. Alphabetical sorting makes the list feel static and less useful for someone trying to pick up where they left off or see what has been added lately. Newest-first also makes the feature feel more responsive and current in a community-driven app like CineLog.
**Engagement with reviewer's point:** I think the reviewer’s point is strong because a watchlist is not a catalog; it is a working list. Showing the most recent additions first better reflects how users will actually interact with it, and it makes the list more actionable than a simple title-based ordering.

## Comment 6 — Rebase
**What conflicted:**
**How I resolved it:**
**How I verified no conflict remains:**

## PR Description
This PR adds the watchlist flow to CineLog with the renamed `add_to_watchlist()` entry point, duplicate-entry protection, and tests covering both nonexistent-film and duplicate-entry behavior. It also documents the intended visibility choice and keeps the watchlist behavior aligned with the existing collection patterns.
