# spring-sleuth-feign-issue

Run the Spring Boot application and it will fail with the following stack trace:

```bash
org.springframework.beans.factory.UnsatisfiedDependencyException: Error creating bean with name 'controller': Unsatisfied dependency expressed through method 'setTestService' parameter 0; nested exception is org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'testService' defined in class path resource [com/example/demo/Config.class]: Bean instantiation via factory method failed; nested exception is org.springframework.beans.BeanInstantiationException: Failed to instantiate [com.example.demo.TestService]: Factory method 'testService' threw exception; nested exception is java.lang.IllegalStateException: @Bean method Config.httpClient called as bean reference for type [feign.okhttp.OkHttpClient] but overridden by non-compatible bean instance of type [org.springframework.cloud.sleuth.instrument.web.client.feign.LazyClient$$EnhancerBySpringCGLIB$$74b54b48]. Overriding bean of same name declared in: class path resource [com/example/demo/Config.class]
	at org.springframework.beans.factory.annotation.AutowiredAnnotationBeanPostProcessor$AutowiredMethodElement.inject(AutowiredAnnotationBeanPostProcessor.java:676) ~[spring-beans-5.1.3.RELEASE.jar:5.1.3.RELEASE]
	at org.springframework.beans.factory.annotation.InjectionMetadata.inject(InjectionMetadata.java:90) ~[spring-beans-5.1.3.RELEASE.jar:5.1.3.RELEASE]
	at org.springframework.beans.factory.annotation.AutowiredAnnotationBeanPostProcessor.postProcessProperties(AutowiredAnnotationBeanPostProcessor.java:374) ~[spring-beans-5.1.3.RELEASE.jar:5.1.3.RELEASE]
	at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.populateBean(AbstractAutowireCapableBeanFactory.java:1378) ~[spring-beans-5.1.3.RELEASE.jar:5.1.3.RELEASE]
	at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.doCreateBean(AbstractAutowireCapableBeanFactory.java:575) ~[spring-beans-5.1.3.RELEASE.jar:5.1.3.RELEASE]
	at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.createBean(AbstractAutowireCapableBeanFactory.java:498) ~[spring-beans-5.1.3.RELEASE.jar:5.1.3.RELEASE]
	at org.springframework.beans.factory.support.AbstractBeanFactory.lambda$doGetBean$0(AbstractBeanFactory.java:320) ~[spring-beans-5.1.3.RELEASE.jar:5.1.3.RELEASE]
	at org.springframework.beans.factory.support.DefaultSingletonBeanRegistry.getSingleton(DefaultSingletonBeanRegistry.java:222) ~[spring-beans-5.1.3.RELEASE.jar:5.1.3.RELEASE]
	at org.springframework.beans.factory.support.AbstractBeanFactory.doGetBean(AbstractBeanFactory.java:318) ~[spring-beans-5.1.3.RELEASE.jar:5.1.3.RELEASE]
	at org.springframework.beans.factory.support.AbstractBeanFactory.getBean(AbstractBeanFactory.java:199) ~[spring-beans-5.1.3.RELEASE.jar:5.1.3.RELEASE]
	at org.springframework.beans.factory.support.DefaultListableBeanFactory.preInstantiateSingletons(DefaultListableBeanFactory.java:846) ~[spring-beans-5.1.3.RELEASE.jar:5.1.3.RELEASE]
	at org.springframework.context.support.AbstractApplicationContext.finishBeanFactoryInitialization(AbstractApplicationContext.java:863) ~[spring-context-5.1.3.RELEASE.jar:5.1.3.RELEASE]
	at org.springframework.context.support.AbstractApplicationContext.refresh(AbstractApplicationContext.java:546) ~[spring-context-5.1.3.RELEASE.jar:5.1.3.RELEASE]
	at org.springframework.boot.SpringApplication.refresh(SpringApplication.java:775) [spring-boot-2.1.1.RELEASE.jar:2.1.1.RELEASE]
	at org.springframework.boot.SpringApplication.refreshContext(SpringApplication.java:397) [spring-boot-2.1.1.RELEASE.jar:2.1.1.RELEASE]
	at org.springframework.boot.SpringApplication.run(SpringApplication.java:316) [spring-boot-2.1.1.RELEASE.jar:2.1.1.RELEASE]
	at org.springframework.boot.SpringApplication.run(SpringApplication.java:1260) [spring-boot-2.1.1.RELEASE.jar:2.1.1.RELEASE]
	at org.springframework.boot.SpringApplication.run(SpringApplication.java:1248) [spring-boot-2.1.1.RELEASE.jar:2.1.1.RELEASE]
	at com.example.demo.DemoApplication.main(DemoApplication.java:10) [classes/:na]
Caused by: org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'testService' defined in class path resource [com/example/demo/Config.class]: Bean instantiation via factory method failed; nested exception is org.springframework.beans.BeanInstantiationException: Failed to instantiate [com.example.demo.TestService]: Factory method 'testService' threw exception; nested exception is java.lang.IllegalStateException: @Bean method Config.httpClient called as bean reference for type [feign.okhttp.OkHttpClient] but overridden by non-compatible bean instance of type [org.springframework.cloud.sleuth.instrument.web.client.feign.LazyClient$$EnhancerBySpringCGLIB$$74b54b48]. Overriding bean of same name declared in: class path resource [com/example/demo/Config.class]
	at org.springframework.beans.factory.support.ConstructorResolver.instantiate(ConstructorResolver.java:627) ~[spring-beans-5.1.3.RELEASE.jar:5.1.3.RELEASE]
	at org.springframework.beans.factory.support.ConstructorResolver.instantiateUsingFactoryMethod(ConstructorResolver.java:456) ~[spring-beans-5.1.3.RELEASE.jar:5.1.3.RELEASE]
	at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.instantiateUsingFactoryMethod(AbstractAutowireCapableBeanFactory.java:1288) ~[spring-beans-5.1.3.RELEASE.jar:5.1.3.RELEASE]
	at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.createBeanInstance(AbstractAutowireCapableBeanFactory.java:1127) ~[spring-beans-5.1.3.RELEASE.jar:5.1.3.RELEASE]
	at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.doCreateBean(AbstractAutowireCapableBeanFactory.java:538) ~[spring-beans-5.1.3.RELEASE.jar:5.1.3.RELEASE]
	at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.createBean(AbstractAutowireCapableBeanFactory.java:498) ~[spring-beans-5.1.3.RELEASE.jar:5.1.3.RELEASE]
	at org.springframework.beans.factory.support.AbstractBeanFactory.lambda$doGetBean$0(AbstractBeanFactory.java:320) ~[spring-beans-5.1.3.RELEASE.jar:5.1.3.RELEASE]
	at org.springframework.beans.factory.support.DefaultSingletonBeanRegistry.getSingleton(DefaultSingletonBeanRegistry.java:222) ~[spring-beans-5.1.3.RELEASE.jar:5.1.3.RELEASE]
	at org.springframework.beans.factory.support.AbstractBeanFactory.doGetBean(AbstractBeanFactory.java:318) ~[spring-beans-5.1.3.RELEASE.jar:5.1.3.RELEASE]
	at org.springframework.beans.factory.support.AbstractBeanFactory.getBean(AbstractBeanFactory.java:199) ~[spring-beans-5.1.3.RELEASE.jar:5.1.3.RELEASE]
	at org.springframework.beans.factory.config.DependencyDescriptor.resolveCandidate(DependencyDescriptor.java:273) ~[spring-beans-5.1.3.RELEASE.jar:5.1.3.RELEASE]
	at org.springframework.beans.factory.support.DefaultListableBeanFactory.doResolveDependency(DefaultListableBeanFactory.java:1237) ~[spring-beans-5.1.3.RELEASE.jar:5.1.3.RELEASE]
	at org.springframework.beans.factory.support.DefaultListableBeanFactory.resolveDependency(DefaultListableBeanFactory.java:1164) ~[spring-beans-5.1.3.RELEASE.jar:5.1.3.RELEASE]
	at org.springframework.beans.factory.annotation.AutowiredAnnotationBeanPostProcessor$AutowiredMethodElement.inject(AutowiredAnnotationBeanPostProcessor.java:668) ~[spring-beans-5.1.3.RELEASE.jar:5.1.3.RELEASE]
	... 18 common frames omitted
Caused by: org.springframework.beans.BeanInstantiationException: Failed to instantiate [com.example.demo.TestService]: Factory method 'testService' threw exception; nested exception is java.lang.IllegalStateException: @Bean method Config.httpClient called as bean reference for type [feign.okhttp.OkHttpClient] but overridden by non-compatible bean instance of type [org.springframework.cloud.sleuth.instrument.web.client.feign.LazyClient$$EnhancerBySpringCGLIB$$74b54b48]. Overriding bean of same name declared in: class path resource [com/example/demo/Config.class]
	at org.springframework.beans.factory.support.SimpleInstantiationStrategy.instantiate(SimpleInstantiationStrategy.java:185) ~[spring-beans-5.1.3.RELEASE.jar:5.1.3.RELEASE]
	at org.springframework.beans.factory.support.ConstructorResolver.instantiate(ConstructorResolver.java:622) ~[spring-beans-5.1.3.RELEASE.jar:5.1.3.RELEASE]
	... 31 common frames omitted
Caused by: java.lang.IllegalStateException: @Bean method Config.httpClient called as bean reference for type [feign.okhttp.OkHttpClient] but overridden by non-compatible bean instance of type [org.springframework.cloud.sleuth.instrument.web.client.feign.LazyClient$$EnhancerBySpringCGLIB$$74b54b48]. Overriding bean of same name declared in: class path resource [com/example/demo/Config.class]
	at org.springframework.context.annotation.ConfigurationClassEnhancer$BeanMethodInterceptor.resolveBeanReference(ConfigurationClassEnhancer.java:418) ~[spring-context-5.1.3.RELEASE.jar:5.1.3.RELEASE]
	at org.springframework.context.annotation.ConfigurationClassEnhancer$BeanMethodInterceptor.intercept(ConfigurationClassEnhancer.java:366) ~[spring-context-5.1.3.RELEASE.jar:5.1.3.RELEASE]
	at com.example.demo.Config$$EnhancerBySpringCGLIB$$8bd17196.httpClient(<generated>) ~[classes/:na]
	at com.example.demo.Config.testService(Config.java:63) ~[classes/:na]
	at com.example.demo.Config$$EnhancerBySpringCGLIB$$8bd17196.CGLIB$testService$1(<generated>) ~[classes/:na]
	at com.example.demo.Config$$EnhancerBySpringCGLIB$$8bd17196$$FastClassBySpringCGLIB$$3319d14b.invoke(<generated>) ~[classes/:na]
	at org.springframework.cglib.proxy.MethodProxy.invokeSuper(MethodProxy.java:244) ~[spring-core-5.1.3.RELEASE.jar:5.1.3.RELEASE]
	at org.springframework.context.annotation.ConfigurationClassEnhancer$BeanMethodInterceptor.intercept(ConfigurationClassEnhancer.java:363) ~[spring-context-5.1.3.RELEASE.jar:5.1.3.RELEASE]
	at com.example.demo.Config$$EnhancerBySpringCGLIB$$8bd17196.testService(<generated>) ~[classes/:na]
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method) ~[na:1.8.0_131]
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62) ~[na:1.8.0_131]
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43) ~[na:1.8.0_131]
	at java.lang.reflect.Method.invoke(Method.java:498) ~[na:1.8.0_131]
	at org.springframework.beans.factory.support.SimpleInstantiationStrategy.instantiate(SimpleInstantiationStrategy.java:154) ~[spring-beans-5.1.3.RELEASE.jar:5.1.3.RELEASE]
	... 32 common frames omitted
```