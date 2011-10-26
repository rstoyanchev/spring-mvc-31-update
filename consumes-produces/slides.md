
!SLIDE subsection
# Consumes/Produces

!SLIDE incremental bullets small transition=fade
# Input Media Type

    @@@ java

    @ResponseBody
    @RequestMapping(
            method=RequestMethod.POST,
            header="Content-Type=application/json")

    public String save(@RequestBody JavaBean javaBean) {

    }

!SLIDE incremental bullets small transition=fade
# Input Media Type

    @@@ java

    @ResponseBody
    @RequestMapping(
            method=RequestMethod.POST, 
            consumes="application/json")

    public String save(@RequestBody JavaBean javaBean) {

    }


!SLIDE incremental bullets
# The Moving Parts

* `headers="Content-Type=text/plain"`
* is converted to `consumes="text/plain"`
* Same semantics

!SLIDE incremental bullets small transition=fade
# Output Media Type

    @@@ java

        @ResponseBody
        @RequestMapping(
            method=RequestMethod.GET
            header="Accept=application/json")

        public JavaBean get() {

        }

!SLIDE incremental bullets small transition=fade
# Output Media Type

    @@@ java

        @ResponseBody
        @RequestMapping(
            method=RequestMethod.GET, 
            produces="application/json") 

        public JavaBean get() {

        }

!SLIDE incremental bullets
# The Moving Parts

* `headers="Accept=text/plain"` 
* is converted to `produces="text/plain"`
* Refined semantics
* Aligned with JAX-RS

!SLIDE incremental bullets
# Semantics

* `"Produces"` used not only for mapping
* Affects the actual content type written
* Accepts more general media type

!SLIDE incremental bullets small
# For Example

* Request for `"text/*"`
* Matches to method `produces = "text/plain"`
* So does a request for `"*/*"`
* And so does a request without `Accept` header

!SLIDE incremental bullets small
# Another Example

* `produces = "application/json" `
* Request for `"*/*"`
* Content type written is `"application/json"`
* Not any configured message converter

!SLIDE incremental bullets small
# Yet Another Example

* `produces = "text/plain;charset=UTF-8"`
* Request for `"text/plain"`
* Content type written is `"text/plain;charset=UTF-8"`
* Matches producible type

!SLIDE incremental small
# What About?
<br><br>
##Request for `"*/*"` (or without Accept) header

    @@@ java

        @RequestMapping 
        public String get(Model model) {


        }

        @ResponseBody
        @RequestMapping(produces="application/json") 
        public JavaBean get() {

        }

!SLIDE incremental  small
# What About?
<br><br>
##Request for `"*/*"` (or without Accept) header

    @@@ java

        @RequestMapping 
        public String get(Model model) {
            // This method is chosen

        }

        @ResponseBody
        @RequestMapping(produces="application/json") 
        public JavaBean get() {

        }


!SLIDE incremental  small
# What About?
<br><br>
##Request for `"*/*"` (or without Accept) header

    @@@ java

        @RequestMapping 
        public String get(Model model) {
            // This method is chosen
            // As a match to '*/*'
        }

        @ResponseBody
        @RequestMapping(produces="application/json") 
        public JavaBean get() {

        }

!SLIDE
# Code Samples
<br><br>
<a href="https://github.com/SpringSource/spring-mvc-showcase">__https://github.com/SpringSource/spring-mvc-showcase__</a>
<br>
<a href="https://github.com/SpringSource/spring-mvc-showcase/blob/master/src/main/java/org/springframework/samples/mvc/mapping/MappingController.java">MappingController.java</a><br><br>
<a href="https://github.com/SpringSource/spring-mvc-showcase/blob/master/src/main/java/org/springframework/samples/mvc/response/ResponseController.java">ResponseController.java</a>


