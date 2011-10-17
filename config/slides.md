
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

!SLIDE smaller
# Example

	@@@ xml

    <annotation-driven />


	<mvc:interceptors>
		<ref bean="log4jInterceptor"/>
	</mvc:interceptors>


    <resources mapping="/resources/**" location="/resources/" />


    <mvc:default-servlet-handler />    

!SLIDE incremental
# Namespace Challenges
.notes Ask how many people use the namespace? Probably under 50% ...

* Black box
* All or nothing proposition
* How do I customize bean property "xyz" ?

!SLIDE incremental
# MVC Java Config

* Code-based alternative
* Not a one-for-one "translation"
* Matches the benefits of the namespace
* Addresses the shortcomings

!SLIDE smaller
# Basic MVC Java Config
# Example

	@@@ java

    @Configuration
    @EnableWebMvc
    public class WebConfig extends WebMvcConfigurerAdapter {

      @Override
	  public void addFormatters(FormatterRegistry registry){
          // ...
	  }

	  @Override
	  public void addInterceptors(InterceptorRegistry registry){
          // ...
	  }

    }

!SLIDE smaller
# Plugging Java config via web.xml

	@@@ xml

    <context-param>
        <param-name>contextClass</param-name>
        <param-value>
            org.springframework.web.context.support.
             AnnotationConfigWebApplicationContext
        </param-value>
    </context-param>

    <context-param>
        <param-name>contextConfigLocation</param-name>
        <param-value>
            org.springframework.samples.mvc31.config
        </param-value>
    </context-param>

!SLIDE incremental
# Why MVC Java Config?

* Convenient chained-method API
* IDE shortcuts, Javadoc, etc.
* Transparent
* Advanced customizations possible

!SLIDE smaller
# Advanced Customizations

	@@@ java

    @Configuration
    public class WebConfig extends WebMvcConfigurationSupport {

      @Override
	  public void addFormatters(FormatterRegistry registry){
          // ...
	  }

      @Override
      public RequestMappingHandlerAdapter 
                  requestMappingHandlerAdapter() {

          // Create or let "super" create and customize 
          // RequestMappingHandlerAdapter ...

      }
    }

!SLIDE code
# Demo 


__Basic config:__<br>
https://github.com/SpringSource/greenhouse
 
__Advanced customizations:__<br>
https://github.com/rstoyanchev/spring-mvc-31-demo



