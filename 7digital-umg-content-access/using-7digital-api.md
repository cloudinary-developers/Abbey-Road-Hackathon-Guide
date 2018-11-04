# Using 7digital API

## Overview

**Universal Music Group have made a some of their songs available for the Abbey Road Red hackathon**

* ≈ 20,000 songs
* ≈ 1,500 unique artists
* ≈ 5,000 albums/singles
* Covers many genres, rock, pop, country....etc
* Spans each decade from 1960's to present

**7digital have activated some of their API endpoints to get access to the UMG catalog**

* Browse catalog and discover artists, albums and tracks
* Get data for artists, albums and tracks - artist name, album title, track name
* Retrieve album artwork \(CD covers\) for every album in the catalog
* Stream full length audio files for every song in the catalog

## API Architecture <a id="api-architecture"></a>

![](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LMw7rB6tN87JH_K_qhA%2F-LMwD1UzpvNzajWkgi6a%2F-LMwIvwUUzcirU0BfUue%2FScreen%20Shot%202018-09-21%20at%2014.26.15.png?alt=media&token=81fbb381-48d4-42e1-b095-abfd1ba61346)

## Catalog Schema <a id="catalog-schema"></a>

![](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LMw7rB6tN87JH_K_qhA%2F-LMwJ5tFgIIrT6EIKcxI%2F-LMwJqfMuRaZCPrkgRcX%2FScreen%20Shot%202018-09-21%20at%2014.30.11.png?alt=media&token=149c79a7-6abb-4b0f-a092-ae80d82e0d0e)

**​**[**List of catalog metadata can be found on this page**](https://cloudinary.gitbook.io/abbey-road-hackathon-2018/7digital/catalog-metadata-available)**​**

## Accessing UMG Catalog using 7digital API <a id="accessing-umg-catalog-using-7digital-api"></a>

**Access to UMG catalog using 7digital services \(API\)**

* Provided through a REST style interface
* Controlled by a consumer key that needs to passed in as a parameter
* **`consumer_key = 7d4vr6cgb392`**
* Identified by a shop identifier that needs to be passed in as a parameter
* **`shopId = 2020`**

**Streaming audio files requires API requests to be signed with an oauth 1.0 signature**

* Sign requests using consumer key and secret
* **`consumer_key = 7d4vr6cgb392`**
* **`consumer_secret = m4ntskavq56rddsa`**

## Sample API Call <a id="sample-api-call"></a>

​[http://api.7digital.com/1.2/artist/search?shopId=2020&oauth\_consumer\_key=7d4vr6cgb392&q=john](http://api.7digital.com/1.2/artist/search?shopId=2020&oauth_consumer_key=7d4vr6cgb392&q=john)​

| Call Components | Meaning |
| :--- | :--- |
| http://api.7digital.com/1.2 | 7digital API site and version |
| artist/search | API endpoint name - search artists |
| ?shopId=2020 | Parameter to identify UMG catalog |
| &oauth\_consumer\_key=7d4vr6cgb392 | Parameter for consumer key |
| &q=john | Parameter for search query string |

## API Endpoint List  <a id="api-endpoint-list"></a>

The following table contains a link to our online documentation for each endpoint, and a sample working call for each endpoint. You can use this to help understand how our calls are constructed and what the responses look like

<table>
  <thead>
    <tr>
      <th style="text-align:left">Endpoint</th>
      <th style="text-align:left">Use</th>
      <th style="text-align:left">Sample Call</th>
      <th style="text-align:left">Main Parameter</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">​<a href="http://docs.7digital.com/#_artist_browse_get">Artist browse</a>​</td>
      <td
      style="text-align:left">Browse the catalog for artist names that start with supplied text string</td>
        <td
        style="text-align:left">​<a href="http://api.7digital.com/1.2/artist/browse?shopId=2020&amp;oauth_consumer_key=7d4vr6cgb392&amp;letter=ki">GET artist/browse</a>​</td>
          <td
          style="text-align:left">letter={text}</td>
    </tr>
    <tr>
      <td style="text-align:left">​<a href="http://docs.7digital.com/#_artist_search_get">Artist search</a>​</td>
      <td
      style="text-align:left">Search the catalog for artists that match a supplied text string</td>
        <td
        style="text-align:left">​<a href="http://api.7digital.com/1.2/artist/search?shopId=2020&amp;oauth_consumer_key=7d4vr6cgb392&amp;q=john">GET artist/search</a>​</td>
          <td
          style="text-align:left">q={text}</td>
    </tr>
    <tr>
      <td style="text-align:left">​<a href="http://docs.7digital.com/#_artist_releases_get">Artist releases</a>​</td>
      <td
      style="text-align:left">Returns a list of streamable releases for a specific artist</td>
        <td style="text-align:left">​<a href="http://api.7digital.com/1.2/artist/releases?shopId=2020&amp;oauth_consumer_key=7d4vr6cgb392&amp;artistId=1448&amp;usageTypes=adsupportedstreaming">GET artist/releases</a>​</td>
        <td
        style="text-align:left">
          <p>&artistId={int}</p>
          <p>&usageTypes=adsupportedstreaming</p>
          </td>
    </tr>
    <tr>
      <td style="text-align:left">​<a href="http://docs.7digital.com/#_artist_toptracks_get">Artist toptracks</a>​</td>
      <td
      style="text-align:left">Returns a list of streamable tracks for a specific artist</td>
        <td style="text-align:left">​<a href="http://api.7digital.com/1.2/artist/toptracks?shopId=2020&amp;oauth_consumer_key=7d4vr6cgb392&amp;artistId=1448&amp;usageTypes=adsupportedstreaming">GET artist/toptracks</a>​</td>
        <td
        style="text-align:left">
          <p>&artistId={int}</p>
          <p>&usageTypes=adsupportedstreaming</p>
          </td>
    </tr>
    <tr>
      <td style="text-align:left">​<a href="http://docs.7digital.com/#_release_search_get">Release search</a>​</td>
      <td
      style="text-align:left">
        <p>Search the catalog for releases</p>
        <p>that match a supplied text string</p>
        </td>
        <td style="text-align:left">​<a href="http://api.7digital.com/1.2/release/search?shopId=2020&amp;oauth_consumer_key=7d4vr6cgb392&amp;q=john&amp;usageTypes=adsupportedstreaming">GET release/search</a>​</td>
        <td
        style="text-align:left">
          <p>&q={text}</p>
          <p>&usageTypes=adsupportedstreaming</p>
          </td>
    </tr>
    <tr>
      <td style="text-align:left">​<a href="http://docs.7digital.com/#_release_tracks_get">Release tracks</a>​</td>
      <td
      style="text-align:left">Returns a list of streamable tracks for a specific release</td>
        <td style="text-align:left">​<a href="http://api.7digital.com/1.2/release/tracks?shopId=2020&amp;oauth_consumer_key=7d4vr6cgb392&amp;releaseId=5726299&amp;usageTypes=adsupportedstreaming">GET release/tracks</a>​</td>
        <td
        style="text-align:left">
          <p>&releaseId={int}</p>
          <p>&usageTypes=adsupportedstreaming</p>
          </td>
    </tr>
    <tr>
      <td style="text-align:left">​<a href="http://docs.7digital.com/#_track_search_get">Track search</a>​</td>
      <td
      style="text-align:left">Search the catalog for releases that match a supplied text string</td>
        <td
        style="text-align:left">​<a href="http://api.7digital.com/1.2/track/search?shopId=2020&amp;oauth_consumer_key=7d4vr6cgb392&amp;q=john&amp;usageTypes=adsupportedstreaming">GET track/search</a>​</td>
          <td
          style="text-align:left">
            <p>&q={text}</p>
            <p>&usageTypes=adsupportedstreaming</p>
            </td>
    </tr>
    <tr>
      <td style="text-align:left">​<a href="http://docs.7digital.com/#_stream_catalogue_get">Track stream</a>​</td>
      <td
      style="text-align:left">Stream full length (or partial clip) audio for a specific track</td>
        <td
        style="text-align:left"><b>See next page</b>
          </td>
          <td style="text-align:left">&trackId={int}</td>
    </tr>
  </tbody>
</table>