## SwiftKitten

SwiftKitten is a Swift autocompleter for Sublime Text, via the adorable 
[SourceKitten](https://github.com/jpsim/SourceKitten.git) framework.


![](demo.gif)


This package is new and still in beta. I welcome any suggestions. If
you find a bug, please open an issue.


### installation

SwiftKitten is not yet available via Package Control (soon hopefully).

To install manually, clone this repository into your packages directory:

`git clone https://github.com/johncsnyder/SwiftKitten.git`

In Sublime, run `Preferences: Browse Packages`  from the command palette 
to find your packages directory. 

### dependencies


#### ijson

SwiftKitten uses [ijson](https://pypi.python.org/pypi/ijson) to parse
completions results from SourceKitten. By default, SwiftKitten will use
the pure python backend. If the faster `yajl2_cffi` backend is available,
SwiftKitten will automatically load it. It is highly recommended that
you build the cffi backend.


#### building cffi [optional]

Navigate to `[Packages]/SwiftKitten/cffi/` and run `python setup.py build`.
This will build cffi in place. Next time you start Sublime, SwiftKitten will
load the `yajl2_cffi` backend.



### caching

SwiftKitten uses [pygments](http://pygments.org) to parse autocomplete
prefixes and caches the result for the next time you request it. There will
be a slight delay the first time you autocomplete a function, but the next
time, it will be instantaneous. For example

![](example.png)

SwiftKitten will remember the autocomplete results for `foo` and cache them.
The next time you type `foo.`, SwiftKitten will return the cached results.
Also, an autocomplete request will be sent if the cached results have timed
out (See `cache_timeout` in package settings). If the results
have changed, SwiftKitten will update the autocomplete window. A default
cache timeout of one second ensures you will always be shown up-to-date results,
while preventing a barrage of unnecessary requests to SourceKitten.

To clear the cache manually, run `SwiftKitten: Clear Cache



### frameworks

SwiftKitten parses your file to find imported frameworks automatically.
SwiftKitten requests and caches framework globals separately, since they
are only needed once and requesting them via SourceKitten can take a while
(20-30 seconds for Foundation).  It is possbile to exclude specific 
frameworks from autocompletion results (See `exclude_framework_globals` in 
package settings).


### settings

See `SwiftKitten.sublime-settings` for more settings and information.
Copy this file to `[Packages]/User` to customize the settings.

Additionally, settings can be overridden in a sublime project file.



