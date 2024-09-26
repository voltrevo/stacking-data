Approx 2500 stacking choices taken from 8 games using

https://github.com/voltrevo/turbostack-game

at revision b66db15 using the dataCollector global.

Some review cleanup was done too.

The `to` board frequently contains complete lines because `.removeClears()` has not yet been called on it.
