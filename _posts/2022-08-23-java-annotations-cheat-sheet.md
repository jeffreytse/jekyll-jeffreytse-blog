---
layout: post
title: Java Annotations Cheat Sheet
subtitle: All annotations in Java world
author: Jeffrey Tse
categories: computer
tags:
  - programming
  - java
  - note
---

This cheat sheet looks at many annotations that a Java developer should
know if they want to use Java, Spring Framework, SpringBoot, Lombok,
Swagger and so on. It covers the most frequently used and perhaps the
most important annotations.

## JAVA

- Standard (Built-in from `java.lang.*`)
  - @Inherited
  - @Target
  - @Documented
  - @Retention
  - @Inject
  - @Named
  - @Singleton
  - @Valid
  - @NotNull
  - @NotEmpty (JAVE EE 8)
  - @NotBlank
  - @Size
  - @Length
  - @Min
  - @Max
  - @AssertTrue
  - @AssertFalse
  - @Pass
  - @Future
  - @Pattern
  - @PostConstruct
  - @PreDestroy
  - @Override
  - @Transient
  - @Deprecated
  - @SuppressWarnings
  - Servlet API (JAVA EE Platform)
    - @WebServlet
    - @WebInitParam
    - @WebFilter
      - Servlet 3.0
    - @WebListener
    - @HandlesTypes
    - @HttpConstraint
    - @HttpMethodConstraint
    - @MultipartConfig
    - @ServletSecurity
  - ...
- Custom (User-defined)

## Spring

- Global
  - @ComponentScan
  - @EnableAutoConfiguration
  - @Autowired
    - spring2.5
  - @Resource(The same as @Autowired)
  - @Qualifier
  - @Bean
  - @Scope
  - @Import
    - Spring 3.0
  - @ImportResource
    - Spring 3.0
  - @Component
  - @Configuration
  - @Service
  - @Repository
  - @PropertySource
  - @Value
- Spring Cloud (MVC)
  - @EnableDiscoveryClient
  - @ControllerAdvice
    - Spring 3.0
  - @Controller
  - @RestController
  - @RequestMapping
  - @RequestParam
  - @PathVariable
  - @SpringQueryMap
  - @ResponseBody
  - @ResponseStatus
  - @GetMapping
  - @PostMapping
  - @Validated
  - @NonNull
  - @Nullable
  - @Required
  - @ModelAttribute
  - @FormatterType
  - @ControllerAdvice
  - @ExceptionHandler
  - @InitBinder
  - @EnableCaching
  - @RefreshScope
  - @ModelAttribute
  - @RequestAttribute
  - @SessionAttribute
- Spring Security
  - @EnableWebSecurity
  - @CrossOrigin
- Spring Data JPA
  - @MappedSuperClass
  - @NoRepositoryBean
  - @Entity
  - @Table
  - @Column
  - @Id
  - @GeneratedValue
  - @SequenceGeneretor
  - @Transient
  - @Basic
  - @JoinColumn
  - @OneToOne
  - @OneToMany
  - @ManyToOne
- Spring Transaction/AOP
  - @Transactional
  - @Aspect
  - @Pointcut
  - @Before
  - @AfterReturning
  - @Around
  - @AfterThrowing
  - @After
- Spring Cache
  - @Cacheable
  - @CacheEvict
- Spring Retry
  - @Retryable
  - @Recover
  - @Backoff
- Spring Boot
  - @SpringBootApplication
    - The same as __@Configuration + @EnableAutoConfiguration + @ComponentScan__
  - @EnableAutoConfiguration
  - @ServletComponentScan
  - @EnableConfigurationProperties
  - @ConfigurationProperties
  - @Profile
  - Conditional Related
    - @Conditional
      - The new annotation added by Spring 4.0 is used to identify a Spring Bean
      or Configuration configuration file, and the configuration is only enabled
      when the specified conditions are met.
    - @ConditionalOnBean
    - @ConditionalOnMissingBean
    - @ConditionalOnClass
    - @ConditionalOnMissingClass
    - @ConditionalOnWebApplication
    - @ConditionalOnNotWebApplication
    - @ConditionalOnProperty
    - @ConditionalOnExpression
    - @ConditionalOnJava
    - @ConditionalOnResource
    - @ConditionalOnJndi
    - @ConditionalOnCloudPlatform
    - @ConditionalOnSingleCandidate
  - @AutoConfigureAfter
  - @AutoConfigureBefore
  - @AutoConfigureOrder
  - ...

## Lombok

- @EqualsAndHashCode
- @Data
- @Getter
- @Setter
- @Value
- @ToString
- @SneakyThrows
- ...

## Swagger

- @ApiOperation
- @ApiModel
- @ApiParam
- @ApiModelProperty
- ...

