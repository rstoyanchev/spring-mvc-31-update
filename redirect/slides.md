
!SLIDE subsection
# Redirect & Flash Attributes

!SLIDE incremental bullets
# Redirect URL

* A redirect string can be URI template
* Expanded from model attrs
* Remaining attrs appended to query
* But only if they're simple type
* .. works but may lead to surprises

.notes Example surprises ROO-2158, SPR-6796

!SLIDE small
# What will the redirect URL be?

    @@@ java


    @Controller
    public class SomeController {






        @RequestMapping(method=POST)
        public String save(Model model) {
            // ...
            return "redirect:/action";
        }
    }

!SLIDE small
# What will the redirect URL be?

    @@@ java


    @Controller
    public class SomeController {

        @ModelAttribute
        public void populate(Model model) {

        }

        @RequestMapping(method=POST)
        public String save(Model model) {
            // ...
            return "redirect:/action";
        }
    }

!SLIDE small
# What will the redirect URL be?

    @@@ java


    @Controller
    public class SomeController {

        @ModelAttribute
        public void populate(Model model) {
            model.addAttribute(..);
        }

        @RequestMapping(method=POST)
        public String save(Model model) {
            // ...
            return "redirect:/action";
        }
    }

!SLIDE small
# What will the redirect URL be?

    @@@ java

    @SessionAttributes(..)
    @Controller
    public class SomeController {

        @ModelAttribute
        public void populate(Model model) {
            model.addAttribute(..);
        }

        @RequestMapping(method=POST)
        public String save(Model model) {
            // ...
            return "redirect:/action";
        }
    }

!SLIDE small
# What Usually Makes Sense ...

    @@@ java

    @RequestMapping(method=POST)
    public String save(Foo foo, Errors errors, 
                       Model model) {

        if (errors.hasErrors()) {
          return "edit";
        }








        return "redirect:/action";
    }

!SLIDE small
# What Usually Makes Sense ...

    @@@ java

    @RequestMapping(method=POST)
    public String save(Foo foo, Errors errors, 
                       Model model) {

        if (errors.hasErrors()) {
          return "edit";
        }

        // Clear the model for redirect scenario
        model.asMap().clear()





        return "redirect:/action";
    }

!SLIDE small
# What Usually Makes Sense ...

    @@@ java

    @RequestMapping(method=POST)
    public String save(Foo foo, Errors errors, 
                       Model model) {

        if (errors.hasErrors()) {
          return "edit";
        }

        // Clear the model for redirect scenario
        model.asMap().clear()

        // Add attributes for redirect
        model.addAttribute("foo", foo.getId());
        model.addAttribute("queryParam", "value");

        return "redirect:/action/{foo}";
    }

!SLIDE incremental bullets 
# `RedirectAttributes`

* A new method argument type
* Used to select attrs for redirect scenario
* Initially empty
* Used instead of model if controller redirects

!SLIDE smaller
# Example

    @@@ java

        @RequestMapping(method=POST)
        public String save(Foo foo, Errors errors, 
                           RedirectAttributes redirectAttrs){

          if (errors.hasErrors()) {
            return "edit"; 
          }

          redirectAttrs.addAttribute("id", foo.getId);
          redirectAttrs.addAttribute("queryParam", "value");

          return "redirect:/action/{id}";

        }

!SLIDE incremental bullets
# Attribute Formatting

* `RedirectAttributes` formats added values with a `DataBinder`
* Makes them eligible for use in the URL
* Recall only simple type attributes appended to query

!SLIDE smaller
# Example

    @@@ java

        @RequestMapping(method=POST)
        public String save(Foo foo, Errors errors, 
                           RedirectAttributes redirectAttrs){




          redirectAttrs.addAttribute("date", new Date());

          return "redirect:/action";

        }

!SLIDE smaller transition=fade
# Example

    @@@ java

        @RequestMapping(method=POST)
        public String save(Foo foo, Errors errors, 
                           RedirectAttributes redirectAttrs){

          // "date" is formatted
          // RedirectView will append it as query param

          redirectAttrs.addAttribute("date", new Date());

          return "redirect:/action";

        }

!SLIDE incremental bullets
# Using `Model` and `RedirectAttributes`
* Both can be used.. in one method

!SLIDE smaller
# Example

    @@@ java

        @RequestMapping
        public String search(String text, 
                             Model model,
                             RedirectAttributes redirectAttrs){

            // Use Model if not redirecting
            // E.g. Ajax request

            // Use RedirectAttrs if redirecting

        }

!SLIDE small
# What About This?

    @@@ java

      @RequestMapping(method=POST)
      public String save(Foo foo, Errors errors){


          // Will the "default" model be used?
          // Or will it be ignored?

          return "redirect:/action";

      }

!SLIDE incremental bullets small
# `"IgnoreDefaultModelOnRedirect"` Property

* `RequestMappingHandlerAdapter`
* Effectively disables use of "default" model on redirect
* Default value is `"false"` by default
* MVC namespace & Java config set it to `"true"` 

!SLIDE incremental
# Flash Attributes

* Attrs temporily stored in the session
* Before a redirect
* Removed immediately after

!SLIDE smaller
# Example

    @@@ java

      @RequestMapping(method=POST)
      public String save(Entity entity, Errors errors, 
                         RedirectAttributes redirectAttrs){

        // ...






        return "redirect:/action";
      }

!SLIDE smaller slide=fade
# Example

    @@@ java

      @RequestMapping(method=POST)
      public String save(Entity entity, Errors errors, 
                         RedirectAttributes redirectAttrs){

        // ...

        redirectAttrs.addFlashAttribute("message", "Success!");




        return "redirect:/action";
      }

!SLIDE smaller slide=fade
# Example

    @@@ java

      @RequestMapping(method=POST)
      public String save(Entity entity, Errors errors, 
                         RedirectAttributes redirectAttrs){

        // ...

        redirectAttrs.addFlashAttribute("message", "Success!");

        // Attribute "message" will be available 
        // in model of controller following the redirect

        return "redirect:/action";
      }

!SLIDE
# Code Samples 
<br>
<a href="https://github.com/SpringSource/spring-mvc-showcase">https://github.com/SpringSource/spring-mvc-showcase</a>
<br>
<a href="https://github.com/SpringSource/spring-mvc-showcase/blob/master/src/main/java/org/springframework/samples/mvc/form/FormController.java">FormController.java</a>


!SLIDE incremental
# Working with Flash Attributes

* Layered support
* In @MVC use `RedirectAttributes`
* Uses `FlashMap` underneath

!SLIDE small
# Static Access to `FlashMap`
## _(Some Code Not In an @Controller)_

    @@@ java

    // Before redirect

    FlashMap flashMap = 
      RequestContextUtils.getOutputFlashMap(request);






    // ..


!SLIDE small transition=fade
# Static Access to `FlashMap`
## _(Some Code Not In an @Controller)_

    @@@ java

    // Before redirect

    FlashMap flashMap = 
      RequestContextUtils.getOutputFlashMap(request);

    // After redirect

    Map<String, String> map = 
      RequestContextUtils.getInputFlashMap(request);

    // ..

!SLIDE incremental bullets
# Pluggable Support

* `FlashMapManager`
* Discovered by `DispatcherServlet`
* Matches requests to `FlashMap` instances
* Stores instances in HTTP session





