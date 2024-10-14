---
layout: post
title: Test Spring Boot API
date: 2024-10-14 09:57 +0200
categories: [Coding, Spring Boot, Testing]
tags: [Spring Boot, JUnit, Testing, API]
description: "Test Spring Boot API with MockMVC"
---
# Test Spring Boot API with MockMVC

When you develop a Spring Boot application, you might want to test your RESTful API endpoints. In this post, I will show you how to test your Spring Boot API using MockMVC.

## MockMVC

MockMVC is a part of the Spring Test framework that provides a way to test Spring MVC controllers. It allows you to test your controllers without starting a full HTTP server. MockMVC provides a fluent API for making requests to your controllers and validating the responses.

## Implementation in Spring Boot

```java
@AutoConfigureMockMvc
@SpringBootTest
class UrlAdministrationControllerTest {  
    @Autowired
    private MockMvc mockMvc;

    @Test
    void testCreateShortUrlWithNullShortUrl() throws Exception {
        UUID uuid = UUID.randomUUID();
        this.mockMvc.perform(put("/shorturls/" + uuid)
                    .param("originalUrl", "https://www.google.com"))
                    .andDo(print())
                    .andExpect(status().isOk())
                    .andExpect(content().string(containsString(uuid.toString())));
    }
}
```
- @AutoConfigureMockMvc: This annotation is used to automatically configure the MockMvc instance.
- @SpringBootTest: This annotation is used to load the Spring application context.
- @Autowired: This annotation is used to inject the MockMvc instance.
(Dependency Injection)

- mockMvc.perform : This method is used to perform an HTTP request to the specified URL.
- put("/shorturls/" + uuid): This method is used to perform a PUT request to the specified URL.
- param("originalUrl", "https://www.google.com"): This method is used to set the request parameter.
- andDo(print()): This method is used to print the request and response details.
- andExpect(status().isOk()): This method is used to assert the response status code.
- andExpect(content().string(containsString(uuid.toString()))): This method is used to assert the response content.

## Sidenote
In an application with multiple controllers, you can even ask for only one to be instantiated by using, for example, @WebMvcTest(HomeController.class). This will only instantiate the HomeController and not the other controllers.

## Conclusion

In this post, I have shown you how to test your Spring Boot API using MockMVC. MockMVC provides a way to test your controllers without starting a full HTTP server. It allows you to make requests to your controllers and validate the responses. I hope this post helps you to test your Spring Boot API effectively.

## Further Reading for testing in Spring Boot
- [Spring Boot Testing Web](https://spring.io/guides/gs/testing-web)
