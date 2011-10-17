
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
* Superceded controller class hierarchy
* Overall __very__ successful

!SLIDE incremental
# Support Classes

* Gradually evolved
* Not very customizable
* Many a JIRA request for flexibility
* Hindered by some legacy design

.notes Duplicated handler method selection, can't split HTTP methods across controllers, etc.

!SLIDE small incremental
# New @MVC Support Classes

* `RequestMappingHandlerMapping`
* `RequestMappingHandlerAdapter`
* `ExceptionHandlerExceptionResolver`

!SLIDE incremental small
# Configuring the 
# New Support Classes

* Enabled by default from the MVC Java config and namespace
* Old classes still available but no new features

!SLIDE center

![support-classes.png](support-classes.png)

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


https://github.com/rstoyanchev/spring-mvc-31-demo





