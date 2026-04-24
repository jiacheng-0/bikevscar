# Bike vs Car

Interactive Singapore rush-hour race visualization comparing a motorbike route with a car route on GrabMaps, from Symphony Suites in Yishun to Grab OneNorth.

## Route data location

The route data is currently embedded in [`index.html`](index.html), not stored in a separate route file.

- Car route: `CAR_POLY` in `index.html`
- Bike route: `MOTO_POLY` in `index.html`
- Decoder: `decodePolyline6()` in `index.html`
- Runtime coordinates: `carCoords` and `motoCoords`, created in `initRace()`

Both route constants are encoded polyline6 strings. The app decodes them into `[longitude, latitude]` coordinate arrays before drawing the route lines and moving the vehicle markers.

The Singapore route inputs, API call shape, route results, and polyline constants are documented in [`readme-sg.md`](readme-sg.md).

## GrabMaps route API

For drawing the Singapore route line, use the GrabMaps direction endpoint:

```txt
GET https://maps.grab.com/api/v1/maps/eta/v1/direction
```

Send one repeated `coordinates` query value per waypoint, using `longitude,latitude` order:

```txt
coordinates=103.84477896796983,1.4349448873426383
coordinates=103.79323336138137,1.291826895879796
overview=full
profile=driving
```

Call the same endpoint again with `profile=motorcycle` to compare motorcycle ETA where supported.

## Route endpoints

| Vehicle | Route constant | Start point | End point |
| --- | --- | --- | --- |
| Car | `CAR_POLY` | `103.84477896796983, 1.4349448873426383` | `103.79323336138137, 1.291826895879796` |
| Bike | `MOTO_POLY` | `103.84477896796983, 1.4349448873426383` | `103.79323336138137, 1.291826895879796` |

Coordinates are written as `longitude, latitude`.

## Finish order

The current Singapore sample durations are:

| Vehicle | Duration |
| --- | ---: |
| Car | `1903.5 s` |
| Motorbike | `2092.9 s` |

The animation is duration-driven. `markFinished()` records whichever vehicle reaches the destination first, so either the car or motorcycle can finish earlier if updated API results make that vehicle faster.

## Current marker behavior

In `initRace()`, the app sets:

```js
const startCoord = carCoords[0];
```

That means both the car and bike markers are initially placed at the car route's first coordinate when the race starts or resets. The visible start and end pins are also based on the car route:

- Start pin: `carCoords[0]`, labeled `Symphony Suites`
- End pin: `carCoords[carCoords.length - 1]`, labeled `Grab OneNorth`

## Updating routes

To change the race route, replace the encoded polyline strings for `CAR_POLY` and/or `MOTO_POLY`, update `CAR_DURATION` and `MOTO_DURATION`, and keep `ROUTE_START`, `ROUTE_DEST`, HUD distances, status labels, and pin labels in sync. If the new bike route should start from its own first coordinate instead of the car route's first coordinate, update the marker initialization logic in `initRace()`.
