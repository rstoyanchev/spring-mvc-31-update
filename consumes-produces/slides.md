
!SLIDE subsection
# Consumes/Produces

!SLIDE incremental bullets small transition=fade
# Consumes

    @@@ java

    @ResponseBody
    @RequestMapping(method=RequestMethod.POST)

    public String save(@RequestBody JavaBean javaBean) {

    }

!SLIDE incremental bullets small transition=fade
# Consumes

    @@@ java

    @ResponseBody
    @RequestMapping(method=RequestMethod.POST, 
                    consumes="application/json")
    public String save(@RequestBody JavaBean javaBean) {

    }


!SLIDE incremental bullets
# Header Condition

* `headers="Content-Type=text/plain"`
* is converted to `consumes="text/plain"`
* Same semantics
* More expressive

!SLIDE incremental bullets small transition=fade
# Produces 

    @@@ java

        @ResponseBody
        @RequestMapping(method=RequestMethod.GET

        public JavaBean get() {

        }

!SLIDE incremental bullets small transition=fade
# Produces 

    @@@ java

        @ResponseBody
        @RequestMapping(method=RequestMethod.GET, 
                        produces="application/json") 
        public JavaBean get() {

        }

!SLIDE incremental bullets
# Header Condition

* `headers="Accept=text/plain"` 
* is converted to `produces="text/plain"`
* Semantics aligned with JAX-RS

!SLIDE incremental bullets
# `Produces` Semantics

* Used not only for mapping
* Influences actual content type written
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
            // This method wins

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
            // This method wins
            // i.e. method matching to '*/*' prefered
        }

        @ResponseBody
        @RequestMapping(produces="application/json") 
        public JavaBean get() {

        }

!SLIDE
# Demo
<br><br>
<a href="https://github.com/SpringSource/spring-mvc-showcase">__https://github.com/SpringSource/spring-mvc-showcase__</a>
<br>
<a href="https://github.com/SpringSource/spring-mvc-showcase/blob/master/src/main/java/org/springframework/samples/mvc/mapping/MappingController.java">MappingController.java</a><br><br>
<a href="https://github.com/SpringSource/spring-mvc-showcase/blob/master/src/main/java/org/springframework/samples/mvc/response/ResponseController.java">ResponseController.java</a>


