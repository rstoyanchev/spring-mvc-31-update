
!SLIDE subsection bullets smaller
# Agenda

* Code-based Config
* __@MVC Support Classes__
* Consumes & Produces
* URI Variables
* Redirect Scenarios
* UriComponentsBuilder
* Multipart Requests

!SLIDE incremental
# @Controllers

* Introduced in Spring 2.5
* Expanded for REST in 3.0
* Replaced controller class hierarchy
* Overall __very__ successful

!SLIDE incremental
# @MVC Support Classes

* Gradually evolved
* Not very customizable
* Many a JIRA request for flexibility
* Hindered by some legacy design

.notes Duplicated handler method selection, can't split HTTP methods across controllers, etc.

!SLIDE incremental
# New, Spring 3.1
# @MVC Support Classes

* `RequestMappingHandlerMapping`
* `RequestMappingHandlerAdapter`
* `ExceptionHandlerExceptionResolver`

!SLIDE center

![support-classes.png](support-classes.png)

!SLIDE incremental
# @MVC Configuration

* __New__ support classes "on"
* ... if using MVC namespace, Java config
* __Old__ support classes still the default
* ... if not using namespace or Java config
* ... no support for new features

.notes Use of namespace is by choice and represents the recommended configuration

!SLIDE center

![resolver-handler-implementations.png](resolver-handler-implementations.png)

!SLIDE incremental
# __HandlerMapping__ Customizations

* Provide custom `RequestCondition`
* Build `RequestMappingInfo` from
  * custom annotations
  * anything (e.g. Groovy DSL)

!SLIDE incremental
# __HandlerAdapter__ Customizations

* Custom argument & return value types
* Extend built-in argument resolvers
* Extend built-in return value handlers
* Design your own method signature

!SLIDE code
# Demo 

<a href="https://github.com/rstoyanchev/spring-mvc-31-demo">https://github.com/rstoyanchev/spring-mvc-31-demo</a>





