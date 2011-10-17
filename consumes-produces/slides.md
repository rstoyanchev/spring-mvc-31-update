
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
  * For example requests for <br>
    `"text/*"`, `"*/*"` 
    match to `@RequestMapping(produces = "text/plain"`)

!SLIDE code
# Demo

https://github.com/SpringSource/spring-mvc-showcase

`MappingController.java`

`ResponseController.java`


