# UMG Creative Metadata API

For this API we have used music information retrieval to extract what we refer to as "creative" metadata from our audio catalogue. For each track in this ~25k subset of UMG-owned tracks an algorithm has extracted information regarding it's musical composition and harmonic structure, taking the form of attributes such as key, mood, tempo, vocal register and genre. This level of analysis provides for a more holistic perspective into the musical fabric of a song. This can be used for a multitude of different applications, such as song recommendation, track separation and sentiment analysis - hence the "creative" part! We look forward to seeing your ideas…

The data will be  available to anyone who would like to use it \(and signed the 7digital API consent form\) as a TSV flat file to download for the duration of the event, along with the necessary documentation/schema.

Notes:

* This is purely a metadata dataset. If participants would like to combine with audio data they are welcome to use the streaming API provided by 7digital
* The is a flat file for teams to parse as the wish, rather than a REST API
* Data is experimental \(non-production ready\)

  Sample dataset attached so teams have an idea what to expect.

{% file src="../.gitbook/assets/creative-metadata-api-sample.tsv" caption="Creative Metadata API SAMPLE" %}

