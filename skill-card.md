# Errand Router

Plan the optimal order for a multi-stop errand run — post office, pharmacy, library, groceries, pickups — respecting opening hours, so you never backtrack across town or arrive at a closed shop.

## What it gives you

- **Optimal stop ordering**: models your errand run as a Traveling Salesperson Problem with Time Windows; solves it with nearest-neighbor construction + 2-opt local search in milliseconds, no external solver needed
- **Time-window awareness**: each stop takes optional opening/closing hours; the itinerary flags stops you'd reach after closing and computes the wait time if arriving early
- **Real travel math**: haversine distance matrix, speed-adjusted drive times, per-stop dwell (service) time, optional return-to-start leg
- **Timed itinerary**: departure time, per-leg drive times, ETAs, total km, total elapsed, wait time — plus batch-friendly JSON output for agents

## Use it when

- "What order should I do these errands in?"
- "Can I hit these 5 stops before they close if I leave at 10?"
- "Route my Saturday pickups and drop-offs"

## Quick start

```bash
python3 scripts/errand_router.py quick --start "home,52.52,13.405" \
  --stop "post office,52.51,13.39,10,09:00,18:00" \
  --stop "pharmacy,52.53,13.42,15" --stop "library,52.54,13.38,10"
python3 scripts/errand_router.py plan --start "home,52.52,13.405,0" \
  --stop "mall,52.49,13.43,45,10:00,20:00" --stop "gym,52.55,13.35,60" \
  --depart 09:30 --speed 22 --json
```

MIT © 2026 Denis Voronin
