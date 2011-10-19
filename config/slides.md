
!SLIDE subsection bullets smaller
# Agenda

* __Code-based Config__
* @MVC Support Classes
* Consumes & Produces
* URI Variables
* Redirect Scenarios
* UriComponentsBuilder
* Multipart Requests

!SLIDE incremental
# The MVC Namespace

* Introduced in Spring 3.0
* More opinionated than built-in defaults
* Aims to simplify typical configuration

.notes A concise way to register: Interceptors, Converters, Formatters, Resource handling, View controllers, and more...

!SLIDE
# Example

	@@@ xml

      <mvc:annotation-driven />

      <mvc:interceptors>
	      <ref bean="log4jInterceptor"/>
      </mvc:interceptors>

      <mvc:resources mapping="/resources/**" 
            location="/resources/" />

      <mvc:default-servlet-handler />    

!SLIDE incremental
# Ease-of-Use vs Control:
# MVC Namespace
.notes Ask how many people use the namespace? Probably under 50% ...

* How do I see actual configuration?
* How do I change bean property ... ?
* No transparency
* No path from simple to advanced

!SLIDE incremental
# Spring MVC Java Config
## (Spring 3.1)

* Code-based alternative to namespace
* Not a one-for-one "translation"
* Match the benefits of the namespace
* Address the shortcomings

!SLIDE smaller
# Basic MVC Java Config
# Example

	@@@ java

    @EnableWebMvc
    @Configuration
    public class WebConfig extends WebMvcConfigurerAdapter {

      @Override
	  public void addFormatters(FormatterRegistry reg){
          // ...
	  }

	  @Override
	  public void addInterceptors(InterceptorRegistry reg){
          // Equivalent to <mvc:interceptors>
	  }

      // Override more base class methods as needed...

    }

!SLIDE smaller
# Load Java config from web.xml

	@@@ xml

      <!-- Detect @Configuration classes in a package -->

      <context-param>
        <param-name>contextConfigLocation</param-name>
        <param-value>org.example.somepackage</param-value>
      </context-param>

      <!-- Use ApplicationContext for Java config -->

      <context-param>
        <param-name>contextClass</param-name>
        <param-value>
            org.springframework.web.context.support.
              AnnotationConfigWebApplicationContext
        </param-value>
      </context-param>

!SLIDE incremental
# Why MVC Java Config?

* Higher level configuration API
* Like MVC namespace
* But much easier to see underlying config
* A path from simple to advanced

!SLIDE smaller
# Advanced Customization Example

	@@@ java

    @Configuration
    public class WebConfig extends WebMvcConfigurationSupport {

      @Override
      public void addInterceptors(InterceptorRegistry reg){
        // Equivalent to <mvc:interceptors>
      }

      @Override
      @Bean
      public RequestMappingHandlerAdapter 
                    requestMappingHandlerAdapter() {

          // Create or let "super" create and customize 
          // RequestMappingHandlerAdapter ...

      }
    }

!SLIDE code
# Demo 

<a href="https://github.com/SpringSource/greenhouse">__https://github.com/SpringSource/greenhouse__</a><br>
_See package:_
<a href="https://github.com/SpringSource/greenhouse/tree/master/src/main/java/com/springsource/greenhouse/config">com.springsource.greenhouse.config</a>
 
<a href="https://github.com/rstoyanchev/spring-mvc-31-demo">__https://github.com/rstoyanchev/spring-mvc-31-demo__</a><br>
_See package:_
<a href="https://github.com/rstoyanchev/spring-mvc-31-demo/tree/master/src/main/java/org/springframework/samples/mvc31/config">org.springframework.samples.mvc31.config</a>

!SLIDE
## For more on 
## __Spring MVC Java Config__
## attend this session:
<br><br><br>
## <a href="http://www.springone2gx.com/conference/chicago/2011/10/session?id=24006">__Configuration Enhancements in Spring 3.1__</a>

Wednesday, 12:45



