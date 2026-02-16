# Mapping Nineteenth-Century Obscenity
An interactive map of addresses published in periodical advertisements by sellers of pornography in Britain, 1822–1870.

## Date Created
2026-02-13

## Author
Sarah Bull

Toronto Metropolitan University

sarah.bull@torontomu.ca

## About the project
This interactive map illustrates a small slice of data from _Periodical Advertising, 1822-1870_, a dataset derived from 581 unique periodical advertisements issued by people who sold sexually explicit literature and images in nineteenth-century Britain. The goal of the dataset, and of _Advertising Pornography, 1822-1870_, the larger project in which it is situated, is to expand scholarly understandings of who sold pornography, what they sold, for how much, when, and where in nineteenth-century Britain. More broadly, it aims to develop better understandings of the trade's development and its changing relationship with other elements of media and culture over time. _Advertising Pornography, 1822-1870_ has been peer reviewed and accepted for publication pending minor revisions in _Nineteenth-Century Data Collective_ (<https://c19datacollective.com/>). It should be available there, through a DOI, and at <https://github.com/sarahebull/advertising_pornography_1822_to_1870> later in 2026.

The map plots 114 georeferenced addresses drawn from periodical advertisements published in Britain between 1822 and 1870. The addresses, names, and dates were extracted from _Periodical Advertising, 1822-1870_. Coordinates were assigned by using the National Library of Scotland's Georeferenced Maps Viewer (<https://maps.nls.uk/geo/>) and a wide variety of secondary sources. In cases where an address still exists, the UK Grid Reference for the address was inputted into the Georeferenced Maps Viewer and an entry associated with the address was plotted using the Search tool. In cases where an address no longer exists, the historical location of the address was determined via secondary research and plotted using a combination of georeferencing with the search tool and manual plotting on a historic, georeferenced map. As many addresses no longer exist, users should keep in mind that the specific geographic reference may be an approximation. Expect accuracy at the street level, but not at the building number level.

The majority of the addresses represented in this map are in central London, concentrated around Holywell Street, the Strand, Fleet Street, Soho, and Holborn. A small number of addresses are located in other British cities including Bristol, Sheffield, Rotherham, Lincoln, and Ramsgate.

The interface for the interactive map was built with Claude Code, using historic georeferenced map layers from the National Library of Scotland and advice for users published at <https://maps.nls.uk/projects/api/>

Updates data and code files were uploaded on 2026-02-16. Changes are described below.  

## Files

| File | Description |
|------|-------------|
| `C19_Obscenity_Map_2.0.html` | Self-contained interactive map (Leaflet + MarkerCluster). Open directly in a browser or embed via iframe. |
| `Advertising_Pornography_Georeferenced_Addresses.csv` | The underlying georeferenced dataset (114 addresses). |
| `README.md` | This file. |

## Data: `Advertising_Pornography_Georeferenced_Addresses.csv`

The CSV contains 114 records with the following variables:

| Variable | Type | Description |
|----------|------|-------------|
| `wkt` | string | Well-Known Text point geometry, e.g. `POINT(-0.117 51.517)` |
| `measure` | string | Coordinate summary string (lon/lat in truncated decimal degrees) |
| `type` | string | Geometry type (always `Point`) |
| `description` | string | Composite label: name, year(s), and address as a single string |
| `easting` | integer | British National Grid easting (metres) |
| `northing` | integer | British National Grid northing (metres) |
| `gridref` | string | Ordnance Survey grid reference, e.g. `TQ 3069 8150` |
| `lon` | float | Longitude (WGS84, decimal degrees) |
| `lat` | float | Latitude (WGS84, decimal degrees) |

Names in the `description` field correspond to the Seller_ID variable in _Periodical Advertising, 1822-1870_ and may be pseudonyms. In some cases, a note on the identity appears in square brackets. Year ranges indicate the span of years in which an address appeared in advertisements issued by the seller.

A corrected version of this file was uploaded on 2026-02-16 with the following changes:

- Name corrections: "Judge Family" (Carlton Road) → "Adolphus Henry Judge"; "Richard Groves" → "Joseph Groves"
- Identifications added in square brackets: Anderson [William Lazenby?], Jackson and Co [Frederick Jackson], Emile Levine [William Frederick Howe and Elizabeth Graham?], Palmer [Henry Cook?], Lampert [Theophilus Sebastian Judge?], Cole [James Brewer?], Felix Danjer [William Dugdale?], J. Brooks and Co [Frederick Hunt], Thomas Ward [Thomas Paine Carlile], Weir [Alexander Weerden?]
- Bracket style standardized from parentheses to square brackets throughout
- Smith split into two entries: 1866 at 2 Vaughn-road and 1867 at 43 Vaughn-road (previously combined)
- Felix Danjer address corrected to 37 1/2 Holywell-Street
- Lampert address clarified to "2 Booksellers' Row [Holywell Street]"
- "James [H. James, Esq]" simplified to "James" to match Seller_ID
- Emile Levine entries consolidated/corrected with one now including both Paris and Wych-street addresses
- 8 coordinate corrections (William Benbow, T.T.T, Mons Louise, Thomas Paine Carlile, William Ward, Edward Duncombe, Edward Dyer, Henry Reynolds)
- 1 entry removed: duplicate Eugene Alfred Judge at "Potter's Bar, London, N." (the "Little Heath, Potter's Bar" entry remains)

## Interactive map: `C19_Obscenity_Map_2.0.html`

The map is a single self-contained HTML file with all data embedded as JSON. It requires no server — open it locally in a browser or host it as a static file.

Features:

- Time slider and histogram for filtering by year (individual year, ±5, ±10, or all years)
- Direct year input box
- Animated playback across the date range
- Marker clustering that breaks apart at higher zoom levels
- Choice of base maps: modern (OpenStreetMap greyscale or colour) and historic Ordinance Survey layers for London

To embed the map on a website, host the HTML file and use an iframe:

```html
<iframe src="C19_Obscenity_Map_2.0.html" width="100%" height="700" style="border:none;" loading="lazy"></iframe>
```
An enhanced version of the map was uploaded on 2026-02-16 with the following features:

- Seller Lookup: A searchable dropdown that lets users select one or more sellers by name. Selected sellers are highlighted with colour-coded markers (drawn from a 10-colour palette), while non-selected markers are dimmed. Each selected seller gets a removable tag, and a "Clear all" button resets the selection.
- Connecting polylines: When a seller is selected, coloured lines connect their addresses in chronological order, tracing their movement across London over time.
- Chronological address summary: A panel below the seller tags lists each selected seller's addresses in date order, showing year ranges and addresses.

### Dependencies (loaded from CDN)

- [Leaflet](https://leafletjs.com/) 1.9.4
- [Leaflet.markercluster](https://github.com/Leaflet/Leaflet.markercluster) 1.5.3
- [Google Fonts](https://fonts.google.com/): Playfair Display, Source Sans 3

## Historic map layers

The interactive map offers several historic Ordnance Survey base layers served as free XYZ tiles by the National Library of Scotland. These provide period-appropriate cartographic context for the London addresses:

- **OS Six-Inch County, 1830s–1880s** (default) — combines Middlesex, Surrey, and Kent county sheets for London-area coverage
- **OS London 1:5280, 1848–51** — town plan of central London
- **OS London 1:1250, 1862–74** — high-detail town plan
- **OS London 1:2500, 1893–96** — detailed town plan

For addresses outside the London area, switch to one of the modern base maps.

Historic georeferenced map layers © [National Library of Scotland](https://maps.nls.uk/), [CC-BY 3.0 Unported](https://creativecommons.org/licenses/by/3.0/).

## Licence

The data and code are published under a CC-BY 4.0 license.

## Citation

Bull, Sarah. 2026. Mapping Nineteenth-Century Obscenity. https://github.com/sarahebull/C19obscenitymap

## Acknowledgements

Historic georeferenced map layers are provided by the National Library of Scotland (https://maps.nls.uk/) and used under the terms of the Creative Commons Attribution 3.0 Unported Licence (https://creativecommons.org/licenses/by/3.0/).
