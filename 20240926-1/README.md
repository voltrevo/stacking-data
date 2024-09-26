Approx 7500 stacking choices taken from about 24 games using

https://github.com/voltrevo/turbostack-game

at revision a3036f3 using the dataCollector global.

Some review cleanup was done too.

The `to` board frequently contains complete lines because `.removeClears()` has not yet been called on it.
