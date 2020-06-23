# micronaut-security-attributes


Brings authentication attributes validation part of controller using annotations.
This is a tiny extension of `micronaut-security` using a new security rule `SecuredAttributesRule` handling `@SecuredAttributes` annotation.
Library is not related to any particular authentication method its target is to handle in generic way authentication attributes available in 
`Authentication` instance. 

For more details check https://docs.micronaut.io/latest/api/io/micronaut/security/authentication/Authentication.html

## Setup

To use the Micronaut’s security capabilities you must have the security dependency on your classpath. For example in `build.gradle`

```groovy
annotationProcessor "io.micronaut:micronaut-security"
compile "io.micronaut:micronaut-security"

compile "com.pulsarix.micronaut:micronaut-security-attributes:1.0.0"
```

## Examples

### Validate authentication attribute using `contains` parameter
```java
@Controller
class Controller{
        @SecuredAttributes(value={
           @Attribute(name="iss", contains={ "appIssuer"}),
        })
        @Get
        public HttpResponse index(){
            // your endpoint code here
        }       
}
```

### Validate authentication attribute using `matches` parameter
```java
@Controller
class Controller{
        @SecuredAttributes(value={
           @Attribute(name="iss", matches="[a-zA-z]+"),
        })
        @Get
        public HttpResponse index(){
            // your endpoint code here
        }       
}
```
  
### Validate multiple authentication attributes using `contains` parameter
```java
@Controller
class Controller{
        @SecuredAttributes(value={
                @Attribute(name="iss", contains={ "appIssuer" }),
                @Attribute(name="scp", contains={"read"})
        })
        @Get
        public HttpResponse index(){
            // your endpoint code here
        }       
}
```

### Validate authentication attribute using custom `validator`
```java
@Controller
class Controller{
        @SecuredAttributes(value={
             @Attribute(validator=ResourceIdScopeValidator.class) 
        })
        @Get("/resource/{id}")
        public HttpResponse index(final @PathVariable String id){
            // your endpoint code here
        }       
}
```
