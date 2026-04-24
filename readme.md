# Bike vs Car

Interactive Jakarta rush-hour race visualization comparing a motorbike route with a car route on GrabMaps.

## Route data location

The route data is currently embedded in [`index.html`](index.html), not stored in a separate route file.

- Car route: `CAR_POLY` in `index.html`
- Bike route: `MOTO_POLY` in `index.html`
- Decoder: `decodePolyline6()` in `index.html`
- Runtime coordinates: `carCoords` and `motoCoords`, created in `initRace()`

Both route constants are encoded polyline6 strings. The app decodes them into `[longitude, latitude]` coordinate arrays before drawing the route lines and moving the vehicle markers.

## Route endpoints

| Vehicle | Route constant | Start point | End point |
| --- | --- | --- | --- |
| Car | `CAR_POLY` | `106.830052, -6.175519` | `106.809180, -6.227424` |
| Bike | `MOTO_POLY` | `106.829249, -6.173127` | `106.773965, -6.192164` |

Coordinates are written as `longitude, latitude`.

## Current marker behavior

In `initRace()`, the app sets:

```js
const startCoord = carCoords[0];
```

That means both the car and bike markers are initially placed at the car route's first coordinate when the race starts or resets. The visible start and end pins are also based on the car route:

- Start pin: `carCoords[0]`, labeled `Monas`
- End pin: `carCoords[carCoords.length - 1]`, labeled `Senayan`

## Updating routes

To change the race route, replace the encoded polyline strings for `CAR_POLY` and/or `MOTO_POLY` in `index.html`. If the new bike route should start from its own first coordinate instead of the car route's first coordinate, update the marker initialization logic in `initRace()`.
