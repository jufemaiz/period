# period

[![GoDoc](https://img.shields.io/badge/api-Godoc-blue.svg)](https://pkg.go.dev/github.com/rickb777/period)
[![Go Report Card](https://goreportcard.com/badge/github.com/rickb777/period)](https://goreportcard.com/report/github.com/rickb777/period)
[![Issues](https://img.shields.io/github/issues/rickb777/period.svg)](https://github.com/rickb777/period/issues)

Package `period` has types that represent ISO-8601 periods of time.

The two core types are 

 * `ISOString` - an ISO-8601 string
 * `Period` - a struct with the seven numbers years, months, weeks, days, hours, minutes and seconds.

These two can be converted to the other.

`Period` also allows various calculations to be made. Its fields each hold up to 19 digits precision.

## Status

The basic API exists but may yet change.

## Upgrading

The old version of this was `github.com/rickb777/date/period`, which had very limited number range and used fixed-point arithmetic.

The new version depends instead on `github.com/govalues/decimal`, which gives a huge (but finite) number range. The new version includes a 'weeks' field, whereas the old version did not (it followed `time.Time` API patterns, which don't have weeks).

These functions have changed:

 * `New` now needs one more input parameter for the weeks field (7 parameters in total)
 * `NewYMD` still exists; there is also `NewYMWD`, which will often be more appropriate.

These methods have changed:

 * `Years`, `Months`, `Weeks`, `Days`, `Hours`, `Minutes` and `Seconds` now return `decimal.Decimal`. They replace the old `YearsFloat`, `MonthsFloat`, `DaysFloat`, `HoursFloat`, `MinutesFloat` and `SecondsFloat` methods.
 * `YearsInt`, `MonthsInt`, `WeeksInt`, `DaysInt`, `HoursInt`, `MinutesInt` and `SecondsInt` were added to obtain the fields as an `int`.
 * `OnlyYMD` is now `OnlyYMWD`
 * The old `ModuloDays` was dropped now that weeks are implemented fully. 
 * `Scale` and `ScaleWithOverflowCheck` have been replaced with `Mul`, which returns the multiplication product and a possible `error`.
