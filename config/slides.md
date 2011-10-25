
!SLIDE subsection
# MVC Java Config

!SLIDE incremental bullets
# Spring MVC
# Configuration Options

* (1) Out-of-the-box defaults
* _i.e. empty `<name>-servlet.xml`_
* (2) MVC Namespace
* `<mvc:annotation-driven />` and friends

!SLIDE incremental bullets
# Out-Of-The-Box Defaults
## (`DispatcherServlet.properties`)

* Minimal, neutral, flexible
* A foundation
* Can be verbose for common tasks

!SLIDE incremental bullets
# MVC Namespace
## _(Added in Spring 3.0)_

* More opinionated
* Targets the 80%
* A starting point
* Minimizes boilerplate
* Transparency, flexibility .. ?

!SLIDE incremental bullets
# MVC Java Config
## (Spring 3.1)

* Designed with this experience in mind
* Transparency is key in MVC config
* So is flexibility
* So is a having simple starting point!

!SLIDE small
# A Simple Starting Point

	@@@ java

        // Equivalent to <mvc:annotation:driven/>

        @EnableWebMvc
        @Configuration
        public class WebConfig {

        }

!SLIDE small
# A Simple Starting Point

	@@@ java

        // Equivalent to <mvc:annotation:driven/>

        @EnableWebMvc   // <-- What's behind ? 
        @Configuration
        public class WebConfig {

        }

!SLIDE small transition=scrollLeft
# `@EnableWebMvc`

    @@@ java

        @Retention(RetentionPolicy.RUNTIME)
        @Import(DelegatingWebMvcConfiguration.class)
        @Target(ElementType.TYPE)
        public @interface EnableWebMvc {

        }

!SLIDE small transition=fade
# `@EnableWebMvc`

    @@@ java


        @Import(DelegatingWebMvcConfiguration.class)

        public @interface EnableWebMvc {

        }


!SLIDE incremental bullets
# Config Customizations

* Implement <a href="http://static.springsource.org/spring/docs/3.1.0.RC1/javadoc-api/org/springframework/web/servlet/config/annotation/WebMvcConfigurer.html">`WebMvcConfigurer`</a>
* Or extend <a href="http://static.springsource.org/spring/docs/3.1.0.RC1/javadoc-api/org/springframework/web/servlet/config/annotation/WebMvcConfigurerAdapter.html">`WebMvcConfigurerAdapter`</a>
* Simple, discoverable config API
* Matches MVC namespace

!SLIDE smaller
# Config Customization Example

	@@@ java

    @EnableWebMvc
    @Configuration
    public class WebConfig {
















    }

!SLIDE smaller
# Config Customization Example

	@@@ java

    @EnableWebMvc
    @Configuration
    public class WebConfig extends WebMvcConfigurerAdapter {
















    }

!SLIDE smaller
# Config Customization Example

	@@@ java

    @EnableWebMvc
    @Configuration
    public class WebConfig extends WebMvcConfigurerAdapter {

      @Override
      protected void addFormatters(FormatterRegistry registry) {
        // ...
      }











    }

!SLIDE smaller
# Config Customizations

	@@@ java

    @EnableWebMvc
    @Configuration
    public class WebConfig extends WebMvcConfigurerAdapter {

      @Override
      protected void addFormatters(FormatterRegistry registry) {
        // ...
      }

      @Override
      public void addInterceptors(InterceptorRegistry reg){
        // Equivalent to <mvc:interceptors>
      }






    }

!SLIDE smaller
# Config Customizations

	@@@ java

    @EnableWebMvc
    @Configuration
    public class WebConfig extends WebMvcConfigurerAdapter {

      @Override
      protected void addFormatters(FormatterRegistry registry) {
        // ...
      }

      @Override
      public void addInterceptors(InterceptorRegistry reg){
        // Equivalent to <mvc:interceptors>
      }

      @Override
      public void addViewControllers(ViewControllerRegistry reg) {
        // Equivalent to <mvc:view-controller>
      }

    }

!SLIDE incremental bullets
# Advanced Customizations

* Remove <a href="http://static.springsource.org/spring/docs/3.1.0.RC1/javadoc-api/org/springframework/web/servlet/config/annotation/EnableWebMvc.html">`@EnableWebMvc`</a>
* Extend <a href="http://static.springsource.org/spring/docs/3.1.0.RC1/javadoc-api/org/springframework/web/servlet/config/annotation/WebMvcConfigurationSupport.html">`WebMvcConfigurationSupport`</a>
* Override the same methods as in `WebMvcConfigurer` 
* Override `@Bean` methods

!SLIDE smaller
# Advanced Customizations

	@@@ java

    @EnableWebMvc
    @Configuration
    public class WebConfig extends WebMvcConfigurerAdapter {

      @Override
      public void addInterceptors(InterceptorRegistry reg){
        // Equivalent to <mvc:interceptors>
      }








      }

    }

!SLIDE smaller
# Advanced Customizations

	@@@ java


    @Configuration
    public class WebConfig extends WebMvcConfigurerAdapter {

      @Override
      public void addInterceptors(InterceptorRegistry reg){
        // Equivalent to <mvc:interceptors>
      }








      }

    }

!SLIDE smaller
# Advanced Customizations

	@@@ java


    @Configuration
    public class WebConfig extends WebMvcConfigurationSupport {

      @Override
      public void addInterceptors(InterceptorRegistry reg){
        // Equivalent to <mvc:interceptors>
      }








      }

    }

!SLIDE smaller
# Advanced Customizations

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



      }

    }

!SLIDE smaller
# Advanced Customizations

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

!SLIDE
## For more on this topic attend:
<br><br>
## <a href="http://www.springone2gx.com/conference/chicago/2011/10/session?id=24006">"Configuration Enhancements in Spring 3.1"</a>
<br>
Today (Wed) @ 12:45



