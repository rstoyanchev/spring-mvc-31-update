
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

* `UriTemplate` the main option in Spring 3.0
* Works but some challenges
* Can not encode all URI components fully
* Not very flexible

.notes SPR-8662, SPR-8403, path segments & query params cannot be encoded fully

!SLIDE incremental
# `UriComponents`
## (Spring 3.1)
* A container for URI components
* Created from String, templated values
* Has expand and encode operations
* Immutable

!SLIDE small incremental
# `UriComponentsBuilder`
## (Spring 3.1)

* A builder for UriComponents
* _`UriComponentsBuilder.fromPath(String)`_
* ... with chained API methods
* _`UriComponentsBuilder.fromUriString(String)`_
* ... equivalent to `new UriTemplate(String)`

!SLIDE small
# Example: URI Components

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
# Example: URI Template String

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
# Redirect URLs 
# with `UriComponentsBuilder`

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



