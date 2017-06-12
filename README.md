Create the API project

$ rails new todos-api --api -T
Tell rails that your project is an API with --api

Initialize the spec directory where your tests will be written
$ rails generate rspec:install

It will create some files and a folder:
create  .rspec
create  spec
create  spec/spec_helper.rb
create  spec/rails_helper.rb

Create a folder for the factory files
$ mkdir spec/factories

Define the configuration of shoulda matchers, rspec and database cleaner at spec/rails_helper.rb

Create the models
$ rails g model Todo title:string created_by:string
$ rails g model Item name:string done:boolean todo:references

There is a relationship between Todo and Item models. One Todo instance has many Items

Create the databases:
$ rails db:create
Created database 'todos_api_with_spec_development'
Created database 'todos_api_with_spec_test'

Run the migrations
$ rails db:migrate
== <timestamps1> CreateTodos: migrating ======================================
-- create_table(:todos)
   -> 0.0197s
== <timestamps1> CreateTodos: migrated (0.0197s) =============================

== <timestamps2> CreateItems: migrating ======================================
-- create_table(:items)
   -> 0.0205s
== <timestamps2> CreateItems: migrated (0.0206s) =============================

Write Todo's and Item's specs

Edit the models to validate the fields and define the relationship

Run the spec you defined
$ rspec


Now create the controllers
$ rails g controller Todos
$ rails g controller Items

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

Create a folder for requests specs and the files for each controller we have
$ mkdir spec/requests
$ touch spec/requests/todos_spec.rb
$ touch spec/requests/items_spec.rb

Now we have to create some factories to provide data for tests
$ touch spec/factories/todos.rb
$ touch spec/factories/items.rb


Write spec/requests
Write controller/concerns/exception_halder.rb, request_spec_helper.rb and response.rb

In request_spec_helper.rb we define a helper to Parse the JSON response

The modules must be included at ApplicationController.rb, as bellow:
class ApplicationController < ActionController::API
  include Response
  include ExceptionHandler
end


Run the tests and check that everything is ok

$ rspec
