
!SLIDE subsection bullets smaller
# Agenda

* Code-based Config
* @MVC Support Classes
* __Consumes & Produces__
* URI Variables
* Redirect Scenarios
* UriComponentsBuilder
* Multipart Requests

!SLIDE incremental smaller
# Consumes & Produces 
# Conditions

    @@@ java

	    @RequestMapping(value="/path"
                        method=RequestMethod.POST, 
                        consumes="application/json")
        @ResponseBody
        public String save(@RequestBody JavaBean javaBean) {
            // ..
        }

	    @RequestMapping(value="/path"
                        method=RequestMethod.GET, 
                        produces="application/json") 
        @ResponseBody
        public JavaBean get() {
            // ..
        }

!SLIDE incremental small
# Media Type Header Conditions:
# Auto-converted

* `headers="Content-Type=text/plain"`
  * becomes `consumes="text/plain"`
* `headers="Accept=text/plain"` 
  * becomes `produces="text/plain"`

!SLIDE incremental small
# Consumes & Produces
# Semantics

* Aligned with JAX-RS
* `produces` influences actual content type used
* Possible to request more general media type
* For example request for `"text/*"` or `"*/*"`
matches to `@RequestMapping(produces = "text/plain"`)

!SLIDE code
# Demo

<a href="https://github.com/SpringSource/spring-mvc-showcase">https://github.com/SpringSource/spring-mvc-showcase</a>

<a href="https://github.com/SpringSource/spring-mvc-showcase/blob/master/src/main/java/org/springframework/samples/mvc/mapping/MappingController.java">`MappingController.java`</a><br>
<a href="https://github.com/SpringSource/spring-mvc-showcase/blob/master/src/main/java/org/springframework/samples/mvc/response/ResponseController.java">`ResponseController.java`</a>


