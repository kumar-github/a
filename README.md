# Spring Boot Actuator

> **Every day is a learning day.**

This project will help you in understanding **Spring Boot Actuator** module step by step. Each concept is covered in-depth and organized as individual git commits. The commits are numbered sequentially starting from `00`, `01`, `02` and so on. You can clone the entire project to your local machine and then start applying commits one by one starting from `00`. This `README.md` file will be updated in every commit and will tell you what has been covered in the specific commit.

## Run Locally

Clone the project

```bash
git clone https://github.com/kumar-github/spring-boot-actuator-demo
```

Go to the project root directory

```bash
cd spring-boot-actuator-demo
```

Start the service

```bash
./mvnw spring-boot:run
```

<br/>

---

---

---

<br/>

This project will help you in understanding **Spring Boot Actuator** module step by step. Each concept is covered in-depth and organized as individual git commits. The commits are numbered sequentially starting from `00`, `01`, `02` and so on. You can clone the entire project to your local machine and then start applying commits one by one starting from `00`. This `README.md` file will be updated in every commit and will tell you what is covered in the specific commit.

## Few things about Spring Boot Actuator

*Spring Boot Actuator* module helps you monitor and manage your application. You can choose to manage and monitor your application by using **HTTP** endpoints or with **JMX**.
Actuator endpoints let you monitor and interact with your application. Spring Boot includes a number of built-in endpoints and lets you add your own.

You can *enable* or *disable* each individual endpoint and *expose* them (make them remotely accessible) over **HTTP** or **JMX**. An endpoint is considered to be *available* when it is both *enabled* and *exposed*. The built-in endpoints are auto-configured only when they are available. Most applications choose exposure over HTTP, where the `ID` of the endpoint and a prefix of `/actuator` is mapped to a URL.
For example, by default, the health endpoint is mapped to `/actuator/health`.

## Complete Reference

[Spring Boot Actuator Reference](https://docs.spring.io/spring-boot/docs/current/reference/html/actuator.html)

<br/>

---

---

---

<br/>

## Commit-00 :sparkles:

*This is the Initial Commit.*

We have created a spring boot project via [Spring Initializr](https://start.spring.io/) with below dependencies.

`spring-boot-starter-web`, `spring-boot-starter-actuator`, `spring-boot-devtools`

At this point, the application can be started and accessed on `http://localhost:9090`. Though accessing `http://localhost:9090` will give you a `Whitelabel Error Page` but that is understandable since we did not map any controller to handle the request.

But we can find the below line logged in the console which is the proof that actuator is enabled.

```console
Exposing 1 endpoint(s) beneath base path '/actuator'
```

<br/>

---

<br/>

## Commit-01 :sparkles:

### Customizing the Management Server Port

By default management endpoints are exposed on the same HTTP port in which the service is running. But it is possible to expose the management endpoints on a different HTTP port, using the `management.server.port` property as below.

```properties
management.server.port=9123
```

### Customizing the Management Endpoint Paths

Sometimes, it is useful to customize the prefix for the management endpoints. For example, our application might already use `/actuator` for another purpose. We can use the `management.endpoints.web.base-path` property to change the prefix for the management endpoint as  below.

```properties
management.endpoints.web.base-path=/admin
```

### Customizing JMX Domain

By default, Spring Boot exposes all management endpoints as **JMX** MBeans under the `org.springframework.boot` (except `shutdown`) domain. You can customize the **JMX** domain under which endpoints are exposed using the `management.endpoints.jmx.domain` property as below.

```properties
management.endpoints.jmx.domain=tech.badprogrammer.app
```

### Enabling/Disabling Endpoints

#### Enabling Endpoints

By default all management endpoints are **enabled** (except `shutdown`). You don't have to do anything extra to enable them. To enable the `shutdown` endpoint, use the `management.endpoint.shutdown.enabled` property as below

~~~properties
management.endpoint.shutdown.enabled=true
~~~

#### Disabling Endpoints

##### Disabling Individual Endpoints

If you want to disable an individual endpoint, you can use the respective `management.endpoint.<ENDPOINT_ID>.enabled` property as below.

~~~properties
management.endpoint.health.enabled=false
management.endpoint.info.enabled=false
~~~

##### Disabling All Endpoints

If you want to disable all the endpoints, you can use the `management.endpoints.enabled-by-default` property as below.

~~~properties
management.endpoints.enabled-by-default=false
~~~

*Note: A **disabled** endpoint will not be exposed neither over **JMX** nor over **HTTP**.*



### Exposing/Hiding JMX Endpoints

#### Exposing JMX Endpoints

All **enabled** endpoints are by default **exposed** over **JMX**. You don't have to do anything extra.

#### Hiding (Not Exposing) JMX Endpoints

##### Hiding Individual JMX Endpoints

If you want to hide (not expose) an individual endpoint over **JMX**, use the `management.endpoints.jmx.exposure.exclude` property as below.

~~~properties
management.endpoints.jmx.exposure.exclude=health,info
~~~

##### Hiding All JMX Endpoints

If you want to hide (not expose) all endpoints over **JMX**, use the `management.endpoints.jmx.exposure.exclude` property as below.

~~~properties
management.endpoints.jmx.exposure.exclude=*
~~~

### Exposing/Hiding HTTP Endpoints

#### Exposing HTTP Endpoints

Although the endpoints are **enabled** by default, they are not exposed over **HTTP** like **JMX**.

##### Exposing Individual HTTP Endpoints

An (*enabled*) endpoint can be exposed over **HTTP** by using the `management.endpoints.web.exposure.include` property as below.

~~~properties
management.endpoints.web.exposure.include=health,info
~~~

##### Exposing All HTTP Endpoints

If you want to expose all the (*enabled*) endpoints over **HTTP**, use the `management.endpoints.web.exposure.include` property as below.

~~~properties
management.endpoints.web.exposure.include=*
~~~

#### Hiding HTTP Endpoints

##### Hiding Individual HTTP Endpoints

If you want to hide (not expose) individual endpoints over **HTTP**, use the `management.endpoints.web.exposure.exclude` property as below.

~~~properties
management.endpoints.web.exposure.exclude=health,info
~~~

##### Hiding All HTTP Endpoints

If you want to hide (not expose) all endpoints over **HTTP**, use the `management.endpoints.web.exposure.exclude` property as below.

~~~properties
management.endpoints.web.exposure.exclude=*
~~~

Note: Both `management.endpoints.web.exposure.exclude` and `management.endpoints.web.exposure.include` properties can be used together to have more fine-grained control over exposing and hiding endpoints.

Note: `management.endpoints.web.exposure.exclude` takes more priority over `management.endpoints.web.exposure.include` if used together. *For example*, you can use `management.endpoints.web.exposure.include=*` to expose all the endpoints and use `management.endpoints.web.exposure.exclude=health,info` to hide specifically `health` and `info`.
