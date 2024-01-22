---

title: api document gem investigation

---

# Purpose
* lazy to create/update api document on other website
* document is easiler to become outdated
* prevent unexpected API changes
* Make API as code, put everything in one place (repo)
* If possible, prefer tools with less effort to learn since OpenAPI spec is quite hard to understand

# Solution
1. auto generate OpenAPI document
2. use CI/CD flow to sync generated document to others, ex: postmane, readme


# Prerequisite
## What is OpenAPI?
* It is a specification which can be used to format the HTTP APIs.
* It will create a JSON format to represent the API's request and response.
## What is the different beteween Swagger and OpenAPI
* Swagger is the implementation of OpenAPI.


# Option
1. [rspec-openapi](https://github.com/exoego/rspec-openapi)
* auto generate OpenAPI document by run rspec
* Pros:
  * auto generated, require less human resource
  * everthing always up to date
  * can run with exist rspec, not need to write new one
* Cons:
  * cannot modified or restricted on particular field when publising. Always the latest version
  * The generate document depends on which rspec is choosen
  * Hard to understand the genenrate document since it is in OpenAPI format

2. [rswag](https://github.com/rswag/rswag)
* generate OpenAPI document by rspec written with DSL
* Pros:
  * a litte easier to understand since it is written in rspec
  * eaiser to control the part you want to publish
* Cons:
  * need to learn new DSL which similar to OpenAPI format
  * only generate document base on what you have written

3. [apipie-rails](https://github.com/Apipie/apipie-rails)
* provide DSL to specify API spec in controller, then generate document base on it
* Pros:
  * easy to understand since it is written in ruby
  * provided validation check for parameter to prevent unexpected change
* Cons:
  * Controller will become a lot fatter
  * everything write from scratch
  * only support swagger version 2, while the latest version is 3
  * personal feeling: the gem requires multiple work around to make things work

# github workflow to check API changes
1. create API with provided method during CI
2. Make a commit with the generate document
3. Now can review the changes on PR
