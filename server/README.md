# Hemisphere Herald live server

This service continuously rotates through every country in `public/countries.geojson`, refreshes the global feed every five minutes, and atomically persists last-known-good records for restart recovery. The public `world-live` endpoint remains unavailable until every country has been attempted once, so the website never switches to a partially bootstrapped server.

The Oracle deployment runs as a restricted system user under `systemd`. It exposes `GET /api/live-news?scope=world-live`, `GET /api/diagnostics/world`, and `GET /healthz`; clicking a country in the website never starts provider work. Each country refresh expands the five leading events plus one rotating event with focused topic searches. A thin first pass automatically expands across additional search feeds when fewer than five distinct matching publishers are found, and the ready-to-read world feed retains up to five sources per priority event.
