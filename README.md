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

Teacher passed use [this site](https://mermaid.js.org/) as the official website who talks about Mermaid.