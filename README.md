Create the API project

Tell rails that your project is an API with --api
```sh
rails new todos-api --api -T
```

Initialize the spec directory where your tests will be written

```sh
rails generate rspec:install
```

It will create some files and a folder:
create  .rspec
create  spec
create  spec/spec_helper.rb
create  spec/rails_helper.rb

Create a folder for the factory files
```sh
mkdir spec/factories
```

Define the configuration of shoulda matchers, rspec and database cleaner at spec/rails_helper.rb

Create the models
```sh
rails g model Todo title:string created_by:string
```
```sh
rails g model Item name:string done:boolean todo:references
```

There is a relationship between Todo and Item models. One Todo instance has many Items

Create the databases:
```sh
rails db:create
```

Created database 'todos_api_with_spec_development'
Created database 'todos_api_with_spec_test'

Run the migrations
```sh
rails db:migrate
```

Write Todo's and Item's specs

Edit the models to validate the fields and define the relationship

Run the spec you defined
```sh
rspec
```

Now create the controllers
```sh
rails g controller Todos
```

```sh
rails g controller Items
```

These commands will create some files:
create  app/controllers/todos_controller.rb
invoke  rspec
create    spec/controllers/todos_controller_spec.rb

create  app/controllers/items_controller.rb
invoke  rspec
create    spec/controllers/items_controller_spec.rb

Define the routes at config/routes.rb
resources :todos do
  resources :items
end

---

## API Routes ##

### Products ###
|   Action                                 | Method    | URL                                               
| -----------------------------------------|-----------|----------------------------------------------------- 
|   List all todos                         |  `GET`    | /todos
|   Create a new todo                      |  `POST`   | /todos
|   Get a todo                  					 |  `GET`    | /todos/:id
|   Update a todo                          |  `PUT`    | /todos/:id
|   Delete a todo and its items            |  `DELETE` | /todos/:id
|   Get a todo item              					 |  `GET`    | /todos/:id/items
|   Update a todo item                     |  `PUT`    | /todos/:id/items
|   Delete a todo item                     |  `DELETE` | /todos/:id/items

---

Create a folder for requests specs and the files for each controller we have
```sh
mkdir spec/requests
```

```sh
touch spec/requests/todos_spec.rb
```
```sh
touch spec/requests/items_spec.rb
```

Now we have to create some factories to provide data for tests
```sh
touch spec/factories/todos.rb
```
```sh
touch spec/factories/items.rb
```

Write spec/requests
Write controller/concerns/exception_halder.rb, request_spec_helper.rb and response.rb

In request_spec_helper.rb we define a helper to Parse the JSON response

The modules must be included at ApplicationController.rb, as bellow:
class ApplicationController < ActionController::API
  include Response
  include ExceptionHandler
end


Run the tests and check that everything is ok

```sh
rspec
```

---

## Contributor

> Danilo Assis Nobre dos Santos Silva ([daniloanobre](https://github.com/daniloanobre)) danilo@lavid.ufpb.br

---