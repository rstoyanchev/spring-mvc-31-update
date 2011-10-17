
!SLIDE subsection bullets smaller
# Agenda

* Code-based Config
* @MVC Support Classes
* Consumes & Produces
* URI Variables
* Redirect Scenarios
* __UriComponentsBuilder__
* Multipart Requests

!SLIDE incremental
# Building a URI

* `UriTemplate` the main option so far
* Works but some challenges
* Can not encode all URI components fully
* Not very flexible

.notes SPR-8662, SPR-8403, path segments & query params cannot be encoded fully

!SLIDE incremental small
# Enter
# `UriComponents`

* A container for URI components
* Created from String, templated values
* Has expand and encode operations
* Immutable

!SLIDE incremental small
# `UriComponentsBuilder`

* A builder for UriComponents
* _`UriComponentsBuilder.fromPath(String)`_
  * with chained API methods
* _`UriComponentsBuilder.fromUriString(String)`_
  * equivalent to `new UriTemplate(String)`

!SLIDE small
# Build From a Path

    @@@ java

        UriComponents uriComponents = 
	        UriComponentsBuilder.fromPath("path")
		        .queryParam("id", "A B")
                .fragment("a")
                .build()
                .encode();

        UriComponents uriComponents = 
	        UriComponentsBuilder.fromPath("path")
		        .query("id={id}")
                .fragment("a")
                .build()
                .expand("A B")
                .encode();

!SLIDE small
# Build From URI String Example

    @@@ java

      UriComponents uriComponents = 
          UriComponentsBuilder
            .fromUriString("path?id={id}#a")
            .build()
            .expand("A B")
            .encode();

      MultiValueMap<String, String> queryMap = 
          uriComponents.getQueryParams();

      assertEquals("path", uriComponents.getPath();
      assertEquals("A%20B", queryMap.get("id"));
      assertEquals("a", uriComponents.getFragment();

!SLIDE incremental
# `UriTemplate & UriUtils`

* Still available
* Both delegate to `UriComponents` and `UriComponentsBuilder`

!SLIDE small
# Using `UriComponentsBuilder`
# In Controller Methods

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



