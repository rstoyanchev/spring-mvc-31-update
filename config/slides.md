
!SLIDE subsection
# Java Config

!SLIDE incremental bullets
# MVC Namespace

* Targets the 80%
* A simple starting point
* Minimizes boilerplate
* Transparency .. ?
* Flexibility .. ?

!SLIDE incremental bullets
# MVC Java Config
## (Spring 3.1)

* Designed with this experience in mind
* Transparency is key in MVC config
* So is flexibility

!SLIDE small
# Simple Starting Point

	@@@ java

        // Equivalent to <mvc:annotation:driven/>

        @EnableWebMvc
        @Configuration
        public class WebConfig {

        }

!SLIDE smaller
# Built-in Customizations

	@@@ java

    @EnableWebMvc
    @Configuration
    public class WebConfig {
















    }

!SLIDE smaller
# Built-in Customizations

	@@@ java

    @EnableWebMvc
    @Configuration
    public class WebConfig extends WebMvcConfigurerAdapter {
















    }

!SLIDE smaller
# Built-in Customizations

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
# Built-in Customizations

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
# Built-in Customizations

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


      // ... more available



    }

!SLIDE incremental bullets
# Advanced Customizations

* Remove <a href="http://static.springsource.org/spring/docs/3.1.0.RC1/javadoc-api/org/springframework/web/servlet/config/annotation/EnableWebMvc.html">`@EnableWebMvc`</a>
* Extend <a href="http://static.springsource.org/spring/docs/3.1.0.RC1/javadoc-api/org/springframework/web/servlet/config/annotation/WebMvcConfigurationSupport.html">`WebMvcConfigurationSupport`</a>

!SLIDE smaller
# Advanced Customizations

	@@@ java

    @EnableWebMvc
    @Configuration
    public class WebConfig extends WebMvcConfigurerAdapter{

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
    public class WebConfig extends WebMvcConfigurerAdapter{

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
    public class WebConfig extends WebMvcConfigurationSupport{

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
    public class WebConfig extends WebMvcConfigurationSupport{

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
    public class WebConfig extends WebMvcConfigurationSupport{

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
## This topic covered in more detail:
<br>
Later Today @ 12:45
<br>
## <a href="http://www.springone2gx.com/conference/chicago/2011/10/session?id=24006">"Configuration Enhancements in Spring 3.1"</a>



