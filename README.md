# Message

To be clear. The content here is a content based on a free course. Noone can reproduce this material. If you wanna to know this material, my advice is to you access the **free** [course](https://web.dio.me/track/coding-the-future-claro-java-spring-boot). And if they end the course or start to ask money to study in the course? Well, this considerations are out of my control, but the DIO material is excelent and the course is amazing! If you acquire a DIO paln, you will have access to amazing courses.  

# General

[Link](https://web.dio.me/lab/publicando-sua-api-rest-na-nuvem-usando-spring-boot-3-java-17-e-railway/learning/138c435a-5be5-450b-a292-cf6ea002f54c?back=/play) of the challenge.


# Github source related to the project

Exploring the names related to the project in a Google search I found [this repository](https://github.com/digitalinnovationone/santander-dev-week-2023-api/).


# Generating the boilerplate

We generated the boilerplate in the [http://start.spring.io](http://start.spring.io) again. I tried to use the configurations more next to the teacher. These was the configurations that I selected:

![Configurations in Spring Initializr](images/configurations-in-spring-initializr.png)

I tried to make the same configuration as the teacher, used `Java 17`, but the Spring Boot version had to be newer because the course was recorded last year.

I had to change the port of the application because I already had an application running in the por 8080. I changed adding a file `application.properties` in the root directory with this content:

```
server.port = 8081
```

I renamed the main class as instructed by the teacher to `Application.java` (in src/main/java/dio/), had some changes in this file to reflect this new name and runned the appplication clicking with the left button over the class `Application.java` and selecting "`Run as > Java Application`".

To see the result, I opened "`http://127.0.0.1:8081`" in a browser and saw an error 404 (ok, an error, but the application was invoked = works).

Teacher saw the dependencied that we selected in Spring Initializr are in the file build.gradle (root directory).

Teacher shared with us [this content](https://www.figma.com/design/0ZsjwjsYlYd3timxqMWlbj/SANTANDER---Projeto-Web%2FMobile?node-id=1421-432) that is in Figma related to the API to be devfeloped.

Teacher developer this general JSON with ideas related to the content in Figma:

![initial json ideas based on figma](images/initial-json-ideas-based-on-figma.png)

Grouping the informations in this JSON and improving:

![grouping the informations in the json and improving](images/grouping-the-informations-in-the-json-and-improving.png)

I found [this json](https://github.com/digitalinnovationone/santander-dev-week-2023-api/blob/main/docs/mocks/find_one.json) in the Github repository of the project.


# Asking help for ChatGPT

As you can see in this image, teacher asked ChatGPT for help. Specifically, to generate a Mermaid diagram:

![asking ChatGPT for help](images/asking-chatgpt-for-help.png)

The answer was:

![ChatGPT answer](images/chatgpt-answer.png)

I got this Mermaid class diagram in the repository of the course and installed the extension "`Markdown Preview Mermaid Support`" to see the preview in VSCode.

```mermaid
classDiagram
  class User {
    -String name
    -Account account
    -Feature[] features
    -Card card
    -News[] news
  }

  class Account {
    -String number
    -String agency
    -Number balance
    -Number limit
  }

  class Feature {
    -String icon
    -String description
  }

  class Card {
    -String number
    -Number limit
  }

  class News {
    -String icon
    -String description
  }

  User "1" *-- "1" Account
  User "1" *-- "N" Feature
  User "1" *-- "1" Card
  User "1" *-- "N" News
```

Teacher passed use [this site](https://mermaid.js.org/) as the official website who talks about Mermaid. Teacher talked us that Mermaid is very powerful, supports several things, like relations and sequence diagram!

When I tried to copy some model classes from the official repository, I run into some problems. I am not very experienced with Gradle and I generated my imports in Spring Initializr. The versions are different, I already experienced a problem like this in an another project. Ok, I can copy some Gradle files from the DIO's repository, but I do not have time now for debugging (really serious). Instead, I forked (optional) the DIO repository [here](https://github.com/andreterceiro/santander-dev-week-2023-api), imported in Eclipse as a Gradle project (option "`Import`" and not open), changed the port of the application in the file `application.properties` and had a success when trying to run the project. Because I do not have too much time now, I will take notes here, I will see the files in that repository, but I will not try to reproduce the results prior to develop me version of the solution that I have to deliver.

I changed the strategy to change the port of the application. I removed the file `application.properties` and inserted the next configuration to the YML file `src/main/resources/application-dev.yml`. I have also to insert a environment variable in `Eclipse` in `Run -> Run configuration -> Environment`:

![environment variable](images/enviroment-variable.png)

To be more clear, the environment variable was:

```
SPRING_PROFILES_ACTIVE = dev
```

**Important**: as you can see in the image, the equals sign do not exists. There are two fields.


# H2 console

To access `H2 Console`, please open the URL "`http://127.0.0.1:8085/h2-console`". The username, password and database that are requeried to connect are in the file `src/main/resources/application-dev.yml` (repository="https://github.com/andreterceiro/santander-dev-week-2023-api").


# Models

Teacher created the models. Please verify every file in the repository (https://github.com/andreterceiro/santander-dev-week-2023-api). Remember, unlike some other MVC implementations, in this strategy of implementation repositories to access databases are used, ok? In this application developed by teacher we have an UserRepository **interface** that extentds **JpaRepository **.


# Service

Teacher created interfaces to be exposedin the "`service`" package and in the subdirectory "`impl`" created the implementations that implements the interfaces. As you can see in the files, the unique implementation class that we have is "`UserServiceImpl.java`" that uses the "`Repository`".

The `UserRepository` is injected in the service by Spring, but we do **not** need am annotation "`@Autowired`".

In [this video](https://youtu.be/Z5QKAiNDhvs) I show an interesting thing that I noted when I watched teacher's videos.


# Controller

Well, `UserController` uses `UserService`. Details:

- The annotation "`@Autowired`" was **not** used;
- `UserController` depends on the **interface** `UserService`, but Spring knows that it have to inject `UserServiceImpl`, who implements `UserService` **interface** and has the "`@Service`" annotation.

The basic annotations:

- **@RestController** in the **class** to the class acts as a REST controller, receiving requests;
- **@RequestMapping("/users"): prefix of the URL used in methods that receives requests, like `users/1`;
- **@GetMapping("/{id}"): obviously ("/{id}") was an example and we have "@PostMapping", "@PutMapping", "@DeleteMapping" etc related to other HTTP verbs.

Remembering how to get a variable through URL:

![path variable](images/path-variable.png)

You can see in the source that maybe the user do not exists, an exception is throwed in the service. The controller uses the service, but as you can see in the previous image it wasn't necessary to catch this exception in the controller.

As you can see in the next image, this is the way we deal with `POST` data, in the `body` of the request, not the URL:

![post request](images/post-request.png)

It was added a Swagger dependency in `build.gradle` file. This dependency is marked as selected in the next image:

![build.gradle](images/swagger-gradle-dependency.png)

This way we can access `http://127.0.0.1:8085/swagger-ui.html`:

![accessing Swagger](images/swagger.png)

As you can see in the next image, several things are created when I create (POST method) a new user:

![several things are created when I POST a new user](images/several-things-created.png)

I do not know exactly why, but to the API works I needed to do not POST the relations `ONE to MANY`. The `JSON` that I posted in `Swagger` was:

```
{
  "name": "Devweekerson",
  "account": {
    "number": "01.097954-4",
    "agency": "2030",
    "balance": 624.12,
    "limit": 1000.00
  },
  "card": {
    "number": "xxxx xxxx xxxx 1111",
    "limit": 2000.00
  }
}
```

I will see the error in future, but this simple JSON that I mentioned above worked to create an user, an account and a card.

I used [this JSON](https://digitalinnovationone.github.io/santander-dev-week-2023-api/mocks/find_one.json) as base removing features and news of the JSON.


# Error messages and exceptions

Teacher created a package under the `controller` package named "`exception`" and there created this "`GlobalExceptionHandler`":

```
package me.dio.controller.exception;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.ExceptionHandler;
import org.springframework.web.bind.annotation.RestControllerAdvice;

import me.dio.service.exception.BusinessException;
import me.dio.service.exception.NotFoundException;

@RestControllerAdvice
public class GlobalExceptionHandler {

    private static final Logger LOGGER = LoggerFactory.getLogger(GlobalExceptionHandler.class);

    @ExceptionHandler(BusinessException.class)
    public ResponseEntity<String> handleBusinessException(BusinessException ex) {
        return new ResponseEntity<>(ex.getMessage(), HttpStatus.UNPROCESSABLE_ENTITY);
    }

    @ExceptionHandler(NotFoundException.class)
    public ResponseEntity<String> hdd-auto-configuration.pngandleNoContentException() {
        return new ResponseEntity<>("Resource ID not found.", HttpStatus.NOT_FOUND);
    }

    @ExceptionHandler(Throwable.class)
    public ResponseEntity<String> handleUnexpectedException(Throwable unexpectedException) {
        String message = "Unexpected server error.";
        LOGGER.error(message, unexpectedException);
        return new ResponseEntity<>(message, HttpStatus.INTERNAL_SERVER_ERROR);
    }
}
```

- See the annotation "`@RestControllerAdvice`";
- See the annotations "`@ExceptionHandler(NotFoundException.class)`" ("NotFoundException" is an example).


# Configuration to production

Teacher instructed us to change the configuration "`ddl-auto`" configuration as I showed in the next image in the first running to "create" and in the following app running to "validate":

![ddl auto configuration](images/ddl-auto-configuration.png)


# Trying to access things in Railway

I installed the Railway CLI this way:

```
bash <(curl -fsSL cli.new)
```

Then I ran the following commands:

```
railway link
railway up
```

I recorded [this initial video](https://youtu.be/gqMaAAW3fAc) about my initial atempts to make the project run on Railway.


# Next attempts trying to run the app on Railway

I accessed [this](https://docs.railway.app/quick-start#deploying-your-project---with-the-cli) documentation.

I ran:

```
railway init
railway run
```

I exposed the service in this page (the interface is a little different now):

![exposing in Railway](images/exposing-in-railway.png)

But when I run the previous commands in CLI, Railway generated the name `"fair-hour"`, ok? This name is on the image.

The URL that Railway passed to me was "http://fair-hour-production.up.railway.app" as you can see in the image.

Then I achieved to access the API in browser using this URL. In port 80, right? I do not know clearly why.

Then I could access `Swagger` in [this URL](https://fair-hour-production.up.railway.app/swagger-ui/index.htm).

I recorded [this video](https://youtu.be/6YjE987Vjfg) about the project working on `Railway`.


# Dealing with a CORS problem

Teacher inserted this `@OpenAPIDefinition` annotation to solve a CORS problem:

![open api definition](images/open-api-definition.png)

Why I didn't experienced the problem? Because I got the final code of the teacher. I forked the DIO repository.


# Some things that I do not know

I do not know why, but when I run the project through Eclipse, the configuration of port (8085) works, but when I run the following command in the root directory (through terminal), the API is exposed on port 8080:

```
./gradlew bootRun
```

I tried to return the "`prd`" configuraton to use Postgres, but i got an error related to a JDBC string (if I remember correctly). I do not try an extensive find of the solution.

In the process of debugging I removed the Tomcat that used the por 8080 from my machine because if I kill the proccess it was restarted and I do ot know how to kill the daemon. The command that I used was:

```
sudo apt-get remove tomcat9
```

Remembering: this is not the Tomcat of the application, that is embedded in the application.
