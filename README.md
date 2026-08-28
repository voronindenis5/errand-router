# Errand Router 🗺️

**Stop zigzagging across town.** Plan the optimal order for a multi-stop errand run — post office, pharmacy, library, groceries, pickups — respecting opening hours, so you never backtrack or arrive at a closed shop.

## The problem

"We need to hit the pharmacy before 6, drop the recycling, grab groceries, and pick up the dry cleaning — what order should we do them in?" Most people solve this by gut feeling and routinely pick an order 20–40% longer than optimal. With opening hours in the mix, a bad order means standing in front of a closed shop.

## The solution

Models your errand run as a **Traveling Salesperson Problem with Time Windows (TSPTW)** and solves it in milliseconds — no external solver, no API calls:

- **Optimal stop ordering** via nearest-neighbor construction + 2-opt local search
- **Time-window awareness**: per-stop opening/closing hours; the itinerary flags stops you'd reach after closing and computes wait time when early
- **Real travel math**: haversine distance matrix, speed-adjusted drive times, per-stop dwell time, optional return-to-start
- **Timed itinerary**: departure time, per-leg drive times, ETAs, total km, total elapsed — plus `--json` for agent pipelines

```bash
python3 scripts/errand_router.py plan --start "home,52.52,13.405,0" \
  --stop "pharmacy,52.51,13.39,10,09:00,20:00" \
  --stop "library,52.54,13.38,15,10:00,18:00" \
  --stop "groceries,52.49,13.43,40,08:00,21:00" \
  --depart 17:00 --speed 22
```

Stdlib-only Python 3. Tests: `python3 scripts/test_errand_router.py`.

MIT © 2026 Denis Voronin
