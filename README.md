# Cache
Dead simple external resource caching (and concatenation). No setup required: automatically creates cache subdirectory and deletes expires files by checking expiration threshold with each request.

Cache takes the following parameters:

### Required
_`url`_ a fully formed URL. This can take a comma-separated list of targets to cache and merge into one output (appended to one another). Pass complex addresses as [percent-encoded](http://meyerweb.com/eric/tools/dencoder/).

_`expire`_ time in seconds until cached file expires (3600 for one minute, 216000 for an hour, etc).

#### Basic example:
<pre>cache/?<em>url=</em><strong>http://swapi.co/api/starships/9/?format=json</strong>&<em>expire=</em><strong>3600</strong></pre>


### Optional

_`json`_ flag to concatenate output if target resources are JSON formatted.

_`direct`_ flag to enable a 302 redirect to the target resource (for the first passed URL). Useful for temporary bypasses of caching during testing.

_`errors`_  flag to include any errors in output. Useful for debugging.

#### Example of multiple combined objects:
<pre>
cache/?<em>url=</em><strong>http://swapi.co/api/starships/9/?format=json</strong><em>,
</em><strong>http://swapi.co/api/people/4/?format=json</strong>
&<em>expire=</em><strong>21600</strong>
</pre>

#### Example of multiple merged objects:
<pre>
  cache/?<em>url=</em><strong>http%3A%2F%2Fswapi.co%2Fapi%2Fplanets%2F%3Fformat%3Djson%26page%3D1</strong><em>,</em>
  <strong>http%3A%2F%2Fswapi.co%2Fapi%2Fplanets%2F%3Fformat%3Djson%26page%3D2</strong><em>,</em>
  <strong>http%3A%2F%2Fswapi.co%2Fapi%2Fplanets%2F%3Fformat%3Djson%26page%3D3</strong>
  <em>&expire=</em><strong>518400</strong><em>&json</em>
</pre>
(URL encoded because the passed URLs themselves have parameters.)

### Todo

- Investigate if there's a better way to match files other than `glob()`.
- Set expires header to match expiry threshold.
- Explore a flag for a 301 rediret to single local file versus loading it in with `file_get_contents()`.
- Evaluate if there's a better way to cache combined and concatenated files.
