# Singapore Route: Symphony Suites to Grab OneNorth

This file records the Singapore route inputs and the Grab Maps results used to generate new `CAR_POLY` and `MOTO_POLY` values for `index.html`.

## Input Places

Start point:

```txt
Entrance Pavilion, Symphony Suites
1 Yishun Close, Singapore, 768004
```

Destination:

```txt
M22 Immersion - Grab OneNorth
3 Media Close, Grab One North, Singapore, 138498
```

## Coordinates

Coordinates are shown as latitude/longitude for readability. The HTTP direction API expects each `coordinates` query value in longitude/latitude order.

| Point | Latitude | Longitude |
| --- | ---: | ---: |
| Entrance Pavilion, Symphony Suites | `1.4349448873426383` | `103.84477896796983` |
| M22 Immersion - Grab OneNorth | `1.291826895879796` | `103.79323336138137` |

## Direction API Calls

Use the resolved coordinates to call the GrabMaps direction endpoint twice:

```txt
GET https://maps.grab.com/api/v1/maps/eta/v1/direction
```

Per the GrabMaps HTTP API reference, send one repeated `coordinates` query value per waypoint in `lng,lat` order. Use `overview=full` so the response includes route geometry for drawing.

```json
{
  "method": "GET",
  "url": "https://maps.grab.com/api/v1/maps/eta/v1/direction",
  "query": {
    "coordinates": [
      "103.84477896796983,1.4349448873426383",
      "103.79323336138137,1.291826895879796"
    ],
    "profile": "driving",
    "overview": "full"
  }
}
```

```json
{
  "method": "GET",
  "url": "https://maps.grab.com/api/v1/maps/eta/v1/direction",
  "query": {
    "coordinates": [
      "103.84477896796983,1.4349448873426383",
      "103.79323336138137,1.291826895879796"
    ],
    "profile": "motorcycle",
    "overview": "full"
  }
}
```

## Route Results

| Vehicle | Profile | Distance | Duration | Geometry |
| --- | --- | ---: | ---: | --- |
| Car | `driving` | `26883.194 m` | `1903.5 s` | polyline6 |
| Motorcycle | `motorcycle` | `26883.194 m` | `2092.9 s` | polyline6 |

Grab returned the same encoded geometry for both `driving` and `motorcycle` for this route, but with different durations. These sample values make the car finish first by `189.4 s`; future calls may differ because the route API can account for current traffic conditions. The app should use the returned durations as data, so either the car or motorcycle can finish earlier.

## Constants for `index.html`

Replace the existing route constants in `index.html` with these values:

```js
const CAR_POLY = "alpvAumcaeEpGsFrM_Lb@_@pJ{InCiCvM_MhBeBxHmFdD{DjBiDnB_GfAsGc@gp@l@uGxAiGjBcFlD{FvEyFrH_I`EqEzCqDfm@gq@~IkKhFgG~KcMxRkTlHqIxCcDnDgC~CoBnCiAbIuBtFy@dLYjIKpKMxH{BxBeBtAqEvAcFb@u[t@{FzAwFpCsFvK{MtMoN~A}GRwCM_F[kBcQoPgQ}PiHmGkBaBmEoE~BmCbAmAlZy]l]ij@hYki@bQe\\dAeBhEiGfHmH|MaKl`@sUbVcMd@WbDwB~P{MrGyGvHwLhHwQpB{FbN}_@vkAwbDxa@_iAly@e{B~HcUpLeSxAkC`ByAlBShNvJnQtJhg@~Udh@vWxQjJtNrHlEzBjU|KhWjLpVjJfYnIfVdFlVtDfZjCvZlAnQVjQ[fb@wAxZeEdWoDvBUp`@kEl[wAxUQpX`@nOz@rTlBr]tF|VrFxVbIlPhHvWvNxJxG|EbDjXdUpPhQ`V~Xb[jc@lMpT|MzUtC~EhTl[paAlaBbXv_@hRtNhO|JfNvGnM|ErAf@nOjDzLjBnOtA|NNpMAfR_A|SqCjVgG~SiIpUgNjFeDtHkFpo@{j@|w@cr@`L}HpM{FxNsDhIk@pHQhR`@dHr@dHdAjIrAdHnBjFt@bP~A|DDpCBhFGhV_CxNkDnE]xPmGpPmGnG{A|NuBnLqAdKUjGEzD^vDfAxhBcHvZ{@xrC}Gdg@mA`aBaCbyAmAr_AQpu@y@vu@QxaCp@zFBtiCp@|v@?rn@aB~a@yApRkBtS_C~WoDjbAwRxw@gQnu@wVdkBqq@|_@eJ`\\kGdYgDfWuBrRo@nZUfV`@fT|@vTtBbUvDrUtEhUtFfUxE`OxCtpE|kAvk@jNtnCxr@x~A~_@dLjCd]`JfUtEjQlCbS`Bfh@xDlz@tA`cBcHvnAaVht@{Ov{Am`@`NaDvo@kOxiAeZpMyC`Im@bb@uKvo@gS`h@_NjR}Ch{Cyu@vfAiYdtAw^jYkFp_@uFt_@qDdDSdEQpe@cAvYi@l]u@lUk@|~@Yzq@kAdQc@tj@mA`LGfhBeClkBCf]bAhNd@|ZdE|X|Enw@~Ux_@bTpP`L~YtWfLpLhg@rj@rNvO`g@|i@`[|\\dHxHfHzHnNbOjGhGlQzMhiA|~@bBtA~FrFlThTjUjWrS|Wxo@reA~JnPnJbQ`Xlv@~Uxn@~^naA`Ld\\bHrS~l@nfBn@xApDvI`KpSbS~[`QbTtMnNlVlUly@vg@vCtA~@^zEnBbCbAfDrAfCdAfBt@`DjA|R`IvJ|CnQjErVxD`eAhNhRfDlZlHdUxHj_@lRhOtKdR|Qp[n^tKvN`f@d|@lNlSjQvSvg@~a@~OjI|Q~FtTrF~KrAbU`BvP~@|Tw@d[}DbLaCzOkErXgNnHyE`J_Hnb@ej@rGsH|NuP~`@_f@nFcH~LeOxUwObUaGdc@uEpb@aAbW?fo@jDza@jBde@aEn`@mPrj@aSxu@}Jpj@}B~_@L~YtExYpJ`q@hVrj@bWndA~b@~w@z^fSpKjQdK`n@xb@t_@t]jHvI~E|GdMfTfD`GrE`K~M|YpPzZtSj^`FxHdU`YhH|HbI|FrPfKbWrMzUfLzSbM`K`I`JtJjKlNnIfPjFjO`FnQtM|f@|Tlx@`Vr|@dKbXtEbKnBvDpJ|SzPl[f^vg@jPlTbNvNzHxHzRxPbS|OfRhMbTzMfOrIfLdIpKdJdOfS|H|PjEtNjDzO~AlTGnUiGz`@kB`I{BzGyTpi@_Orc@_GfO_D|KuHz[wDnTmA`L}AlVm@tMq@hf@m@`T_@bNcFze@sBtPaVfx@ga@xv@}OtYyMhU_FnImOnZgcAnlB_I~O}N`ZmU`o@uNbf@sLjl@mIxk@cFzm@qBln@oFhvBc@zPsF`wBkNfxFoDhq@cFx^sJxa@}Oj`@eUfc@qPtWeXnd@ay@nuAaJpR_HnMic@baA?~BKzAmHtScOd_@oCtGmCpGeBdEeLzVaGbKoFlImJhMiBxBkAbBmA~Ak@g@gCyBeUiTEE_Ay@sRcQoD_EiPyQmSc^{EcEqDsEgCkEeC{CW[sCsCuCgAwCY}CUgEXeF|AyZzRm\\fa@aSlS_B|Fk@fFDh@LhCv@|Cfu@rn@xCr@lAOnAk@v@{@vMyNmAuA}A{A}KqKm@YuCeAeSsPs@k@IDQDQ?QEOKIKCO?I?EBOFMJKNENAN@LDLLHN@RCPv@j@xCdC";
const MOTO_POLY = "alpvAumcaeEpGsFrM_Lb@_@pJ{InCiCvM_MhBeBxHmFdD{DjBiDnB_GfAsGc@gp@l@uGxAiGjBcFlD{FvEyFrH_I`EqEzCqDfm@gq@~IkKhFgG~KcMxRkTlHqIxCcDnDgC~CoBnCiAbIuBtFy@dLYjIKpKMxH{BxBeBtAqEvAcFb@u[t@{FzAwFpCsFvK{MtMoN~A}GRwCM_F[kBcQoPgQ}PiHmGkBaBmEoE~BmCbAmAlZy]l]ij@hYki@bQe\\dAeBhEiGfHmH|MaKl`@sUbVcMd@WbDwB~P{MrGyGvHwLhHwQpB{FbN}_@vkAwbDxa@_iAly@e{B~HcUpLeSxAkC`ByAlBShNvJnQtJhg@~Udh@vWxQjJtNrHlEzBjU|KhWjLpVjJfYnIfVdFlVtDfZjCvZlAnQVjQ[fb@wAxZeEdWoDvBUp`@kEl[wAxUQpX`@nOz@rTlBr]tF|VrFxVbIlPhHvWvNxJxG|EbDjXdUpPhQ`V~Xb[jc@lMpT|MzUtC~EhTl[paAlaBbXv_@hRtNhO|JfNvGnM|ErAf@nOjDzLjBnOtA|NNpMAfR_A|SqCjVgG~SiIpUgNjFeDtHkFpo@{j@|w@cr@`L}HpM{FxNsDhIk@pHQhR`@dHr@dHdAjIrAdHnBjFt@bP~A|DDpCBhFGhV_CxNkDnE]xPmGpPmGnG{A|NuBnLqAdKUjGEzD^vDfAxhBcHvZ{@xrC}Gdg@mA`aBaCbyAmAr_AQpu@y@vu@QxaCp@zFBtiCp@|v@?rn@aB~a@yApRkBtS_C~WoDjbAwRxw@gQnu@wVdkBqq@|_@eJ`\\kGdYgDfWuBrRo@nZUfV`@fT|@vTtBbUvDrUtEhUtFfUxE`OxCtpE|kAvk@jNtnCxr@x~A~_@dLjCd]`JfUtEjQlCbS`Bfh@xDlz@tA`cBcHvnAaVht@{Ov{Am`@`NaDvo@kOxiAeZpMyC`Im@bb@uKvo@gS`h@_NjR}Ch{Cyu@vfAiYdtAw^jYkFp_@uFt_@qDdDSdEQpe@cAvYi@l]u@lUk@|~@Yzq@kAdQc@tj@mA`LGfhBeClkBCf]bAhNd@|ZdE|X|Enw@~Ux_@bTpP`L~YtWfLpLhg@rj@rNvO`g@|i@`[|\\dHxHfHzHnNbOjGhGlQzMhiA|~@bBtA~FrFlThTjUjWrS|Wxo@reA~JnPnJbQ`Xlv@~Uxn@~^naA`Ld\\bHrS~l@nfBn@xApDvI`KpSbS~[`QbTtMnNlVlUly@vg@vCtA~@^zEnBbCbAfDrAfCdAfBt@`DjA|R`IvJ|CnQjErVxD`eAhNhRfDlZlHdUxHj_@lRhOtKdR|Qp[n^tKvN`f@d|@lNlSjQvSvg@~a@~OjI|Q~FtTrF~KrAbU`BvP~@|Tw@d[}DbLaCzOkErXgNnHyE`J_Hnb@ej@rGsH|NuP~`@_f@nFcH~LeOxUwObUaGdc@uEpb@aAbW?fo@jDza@jBde@aEn`@mPrj@aSxu@}Jpj@}B~_@L~YtExYpJ`q@hVrj@bWndA~b@~w@z^fSpKjQdK`n@xb@t_@t]jHvI~E|GdMfTfD`GrE`K~M|YpPzZtSj^`FxHdU`YhH|HbI|FrPfKbWrMzUfLzSbM`K`I`JtJjKlNnIfPjFjO`FnQtM|f@|Tlx@`Vr|@dKbXtEbKnBvDpJ|SzPl[f^vg@jPlTbNvNzHxHzRxPbS|OfRhMbTzMfOrIfLdIpKdJdOfS|H|PjEtNjDzO~AlTGnUiGz`@kB`I{BzGyTpi@_Orc@_GfO_D|KuHz[wDnTmA`L}AlVm@tMq@hf@m@`T_@bNcFze@sBtPaVfx@ga@xv@}OtYyMhU_FnImOnZgcAnlB_I~O}N`ZmU`o@uNbf@sLjl@mIxk@cFzm@qBln@oFhvBc@zPsF`wBkNfxFoDhq@cFx^sJxa@}Oj`@eUfc@qPtWeXnd@ay@nuAaJpR_HnMic@baA?~BKzAmHtScOd_@oCtGmCpGeBdEeLzVaGbKoFlImJhMiBxBkAbBmA~Ak@g@gCyBeUiTEE_Ay@sRcQoD_EiPyQmSc^{EcEqDsEgCkEeC{CW[sCsCuCgAwCY}CUgEXeF|AyZzRm\\fa@aSlS_B|Fk@fFDh@LhCv@|Cfu@rn@xCr@lAOnAk@v@{@vMyNmAuA}A{A}KqKm@YuCeAeSsPs@k@IDQDQ?QEOKIKCO?I?EBOFMJKNENAN@LDLLHN@RCPv@j@xCdC";
```

Because these are polyline6 strings, they work with the existing `decodePolyline6()` helper in `index.html`.
