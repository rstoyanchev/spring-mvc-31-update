
!SLIDE subsection
# UriComponentsBuilder

!SLIDE incremental bullets 
# How To Build a URI

* `UriTemplate`
* Encoding limitations
* Flexible enough .. ?
* Re-usable enough .. ?

.notes SPR-8662, SPR-8403, path segments & query params cannot be encoded fully

!SLIDE incremental bullets
# `UriComponents`

* Immutable container of URI's components
* Provides access to components
* Components may contain URI vars
* Expand/encode operations

!SLIDE small incremental bullets
# How To Create `UriComponents`

* `UriComponentsBuilder.fromPath(String)`
* `UriComponentsBuilder.fromUriString(String)`
* Plus chained builder-style methods

!SLIDE
# Example

    @@@ java



    UriComponents uriComponents = 
      UriComponentsBuilder.fromPath("{path}")
        .queryParam("id", 123)
        .fragment("a")
        .build()
        .expand("/some path")
        .encode();

!SLIDE transition=fade
# Example

    @@@ java
    // Full control over every step
    // vs all in one shot

    UriComponents uriComponents = 
      UriComponentsBuilder.fromPath("{path}")
        .queryParam("id", 123)
        .fragment("a")
        .build()
        .expand("/some path")
        .encode();

!SLIDE incremental bullets
# `UriTemplate & UriUtils` ?

* Still available
* Both use `UriComponents` internally

!SLIDE incremental bullets
# `UriComponents` For Redirect

* An alternative to using `"redirect:"`
* Max control over redirect URL
* Useful in `@ResponseBody` methods too

!SLIDE small
# Example

    @@@ java

    @RequestMapping
    public String handle() {

        // ...

      UriComponents redirectUri = 
          UriComponentsBuilder.fromPath("/path/{id}")
            .query("q={q}")
            .build()
            .expand("123", "q1")
            .encode();

      return "redirect:" + redirectUri.toUriString();

    }



