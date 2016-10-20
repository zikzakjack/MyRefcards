# Spring stereotype annotations

@Component - Indicates that an annotated class is a "component".

@Controller - Indicates that an annotated class is a "Controller"

@Repository - Indicates that an annotated class is a "Repository", originally defined by Domain-Driven Design (Evans, 2003) as "a mechanism for encapsulating storage, retrieval, and search behavior which emulates a collection of objects".

@Service - Indicates that an annotated class is a "Service", originally defined by Domain-Driven Design (Evans, 2003) as "an operation offered as an interface that stands alone in the model, with no encapsulated state."

# Spring context annotations

@Bean - Indicates that a method produces a bean to be managed by the Spring container.

@ComponentScan - Configures component scanning directives for use with @Configuration classes.

@ComponentScan.Filter - Declares the type filter to be used as an include filter or exclude filter.

@ComponentScans - Container annotation that aggregates several ComponentScan annotations.

@Conditional - Indicates that a component is only eligible for registration when all specified conditions match.

@Configuration - Indicates that a class declares one or more @Bean methods and may be processed by the Spring container to generate bean definitions and service requests for those beans at runtime DependsOn - Beans on which the current bean depends.

@EnableAspectJAutoProxy - Enables support for handling components marked with AspectJ's @Aspect annotation, similar to functionality found in Spring's <aop:aspectj-autoproxy> XML element.

@EnableLoadTimeWeaving - Activates a Spring LoadTimeWeaver for this application context

@EnableMBeanExport - Enables default exporting of all standard MBeans from the Spring context, as well as well all @ManagedResource annotated beans.

@Import - Indicates one or more @Configuration classes to import.

@ImportResource - Indicates one or more resources containing bean definitions to import.

@Lazy - Indicates whether a bean is to be lazily initialized.

@Primary - Indicates that a bean should be given preference when multiple candidates are qualified to autowire a single-valued dependency.

@Profile - Indicates that a component is eligible for registration when one or more specified profiles are active.

@PropertySource - Annotation providing a convenient and declarative mechanism for adding a PropertySource to Spring's Environment.

@PropertySources - Container annotation that aggregates several PropertySource annotations.

@Role - Indicates the 'role' hint for a given bean.

@Scope - When used as a type-level annotation in conjunction with @Component, @Scope indicates the name of a scope to use for instances of the annotated type.

# Spring beans annotations

@Autowired - Marks a constructor, field, setter method or config method as to be autowired by Spring's dependency injection facilities.

@Configurable - Marks a class as being eligible for Spring-driven configuration.

@Lookup - An annotation that indicates 'lookup' methods, to be overridden by the container to redirect them back to the BeanFactory for a getBean call.

@Qualifier - This annotation may be used on a field or parameter as a qualifier for candidate beans when autowiring.

@Required - Marks a method (typically a JavaBean setter method) as being 'required': that is, the setter method must be configured to be dependency-injected with a value.

@Value - Annotation at the field or method/constructor parameter level that indicates a default value expression for the affected argument.

