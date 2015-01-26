# NYC Plow History

A very simple (curl + crontab + shell) scraper to keep a history of
[PlowNYC](http://maps.nyc.gov/snow/), New York City's plow tracking map.

## Get the data

The easiest way to get the data is to go to
[openscrape.com/plows/](http://openscrape.com/plows/), where
a timestamped JSON file is stored each time the data changes (every fifteen
minutes).

You can also use git.  While it looks like only the latest data is stored in
`data.json`, it's actually versioned, with this repo automatically updated
every fifteen minutes.  You should be able to get every plow update (excepting
the first few hours) via git's own history after cloning this repo.

## How it works

The script itself is just the `crontab` file.  You'd need to adapt the path to
your machine, as it currently assumes that data will live in
`/home/talos/proj/plows`.

After downloading from the [undocumented GeoJSON endpoint](http://maps.nyc.gov/geoserver/wfs?request=GetFeature&version=1.1.1&typeName=public:SNW_PLOWED&outputFormat=application/json), the JSON is prettified
using `json_pp` and then stripped of procedurally generated feature IDs and
"hours past" measurements using `git`.  This permits clean diffs, as otherwise
those lines would change between commits even if the street wasn't plowed.

## What's next

* Automatically updating [data.beta.nyc](http://data.beta.nyc) with plow data.
* Providing a script to automate the expansion of `data.json` into separate
  versions.

## Thanks

To [Chris Whong](https://github.com/chriswhong) for figuring out the money
endpoint for GeoJSON plow data, and to NYC DoITT for the PlowNYC map.
