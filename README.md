[![General Assembly Logo](https://camo.githubusercontent.com/1a91b05b8f4d44b5bbfb83abac2b0996d8e26c92/687474703a2f2f692e696d6775722e636f6d2f6b6538555354712e706e67)](https://generalassemb.ly/education/web-development-immersive)

# Rails One to Many

Let's build a rails application!

## Objectives

By the end of this, developers should be able to:

- Diagram the database tables and Entity Relationship Diagram that describe a one-to-many relationship.
- Create a new resource using scaffold.
- Write a migration for a one-to-many relationship.
- Compare has_many and belongs_to to other macros, like attr_accessor.
- Configure ActiveRecord to manage one-to-many relationships using has_many and belongs_to.
- Create associated records using the rails console.


## Steps for Adding a Relationship to a Model

1. Generate the new resource it will have a relationship with if needed
1. Add a foreign key to the resource that belongs to the other resource
1. Add relationship macros to both models
1. Update controllers
1. Update views

## Methodical, Error-Driven Development

Status checks will be frequent. As developers we want to be meticulous and make
sure we're getting errors where expected as we build our server.

This is called "error-driven development". The goal is to see an error, and to
learn what error to expect. Embrace the errors, and they will tell you what
your next task is.

Follow the steps outlined in good Error Driven Development

1. Route
    - Test the route, see that a route does not exist
    - Add the route
    - Test the route, see that a route does exist
1. Controller
    - Test the route, see that a route does exist but controller does not
    - Add the controller
    - Test the route, see that a controller exists
1. Model
    - Test the route, see that a controller exists but model does not
    - Add the model
    - Test the route, see that a Model exists
1. Migrations
    - Test the route, see that a Model exists but migrations must be run
    - Run migrations
1. View
    - Test the view, see that it does not exist
    - Add the view
1. Test Feature
    - Test the route, ensure actions are successful
    - Use Rails Console to ensure all data persists as expected
    
## Demo: Books

### User Stories 

- Version 1:
  - As a user, I want to view a single book
  - As a user, I want to view all books
  - As a user, I want to create a book with a title and author
  - As a user, I want to edit a book's title and author
  - As a user, I want to delete a book

- Version 2:
  - As a user, I want to view a single book
  - As a user, I want to view all books
  - As a user, I want to create a book with a title
  - As a user, I want to edit a book's title
  - As a user, I want to delete a book
  - As a user, I want to view an author
  - As a user, I want to view all authors
  - As a user, I want to create an author with a given name and family name
  - As a user, I want to edit an author's given name and family name
  - As a user, I want to delete an author
  - As a user, I want to assign a single author to a book
  - As a user, I want to assign multiple books to an author
  
### Entity Relationship Diagram (ERD) 

#### Version 1

<table>
  <th colspan="2" style="text-align:center">Books</th>
  <tr>
    <td>id</td>
    <td>primary key</td>
  </tr>
  <tr>
    <td>title</td>
    <td>string</td>
  </tr>
  <tr>
    <td>author</td>
    <td>string</td>
  </tr>
  <tr>
    <td>created_at</td>
    <td>datetime</td>
  </tr>
  <tr>
    <td>updated_at</td>
    <td>datetime</td>
  </tr>
</table>

#### Version 2

**Author** has many **Books**

**Books** belong to **Author**

`Authors` -|--< `Books`

<table style="display:inline">
  <th colspan="2" style="text-align:center">Books</th>
  <th colspan="2" style="text-align:center">
  Authors
  </th>
  <tr>
    <td>id</td>
    <td>primary key</td>
    <td>id</td>
    <td>primary key</td>
  </tr>
  <tr>
    <td>title</td>
    <td>string</td>
    <td>first_name</td>
    <td>string</td>
  </tr>
  <tr>
    <th> author_id </th>
    <th> foreign key </th>
    <td>last_name</td>
    <td>string</td>
  </tr>
  <tr>
    <td>created_at</td>
    <td>datetime</td>
    <td>created_at</td>
    <td>datetime</td>
  </tr>
  <tr>
    <td>updated_at</td>
    <td>datetime</td>
    <td>updated_at</td>
    <td>datetime</td>
  </tr>
</table>

## Hospital Example

### User Stories

- Version 1
  - As a user, I want to view a single patient
  - As a user, I want to view all patients
  - As a user, I want to create a patient with a first name, last name,
    diagnosis and born on
  - As a user, I want to edit a patient's first name, last name, diagnosis and
    born on
  - As a user, I want to delete a patient

- Version 2
  - As a user, I want to view a single patient
  - As a user, I want to view all patients
  - As a user, I want to create a patient with a first name, last name,
    diagnosis and born on
  - As a user, I want to edit a patient's first name, last name, diagnosis and
    born on
  - As a user, I want to delete a patient
  - As a user, I want to view a doctor
  - As a user, I want to view all doctors
  - As a user, I want to create a doctor with a given name, family name, zip
    code and specialty
  - As a user, I want to edit a doctor's given name, family name, zip code and
    specialty
  - As a user, I want to delete a doctor
  - As a user, I want to assign a single doctor to a patient
  - As a user, I want to assign multiple patients to a doctor

### Entity Relationship Diagrams

#### Version 1

<table>
  <th colspan="2" style="text-align:center">Patients</th>
  <tr>
    <td>id</td>
    <td>primary key</td>
  </tr>
  <tr>
    <td>first_name</td>
    <td>string</td>
  </tr>
  <tr>
    <td>last_name</td>
    <td>string</td>
  </tr>
  <tr>
    <td>diagnosis</td>
    <td>string</td>
  </tr>
  <tr>
    <td>born_on</td>
    <td>date</td>
  </tr>
  <tr>
    <td>created_at</td>
    <td>datetime</td>
  </tr>
  <tr>
    <td>updated_at</td>
    <td>datetime</td>
  </tr>
</table>

#### Version 2

**Doctor** has many **Patients**

**Patients** belong to **Doctor**

`Patients` -|--< `Doctors`

<table style="display:inline">
  <th colspan="2" style="text-align:center">Patients</th>
  <th colspan="2" style="text-align:center">
  Doctors
  </th>
  <tr>
    <td>id</td>
    <td>primary key</td>
    <td>id</td>
    <td>primary key</td>
  </tr>
  <tr>
    <td>first_name</td>
    <td>string</td>
    <td>first_name</td>
    <td>string</td>
  </tr>
  <tr>
    <td>last_name</td>
    <td>string</td>
    <td>last_name</td>
    <td>string</td>
  </tr>
  <tr>
    <td>diagnosis</td>
    <td>string</td>
    <td>zip_code</td>
    <td>string</td>
  </tr>
  <tr>
    <td>born_on</td>
    <td>date</td>
    <td>specialty</td>
    <td>string</td>
  </tr>
  <tr>
    <th>doctor_id</th>
    <th>foreign key</th>
    <td>created_at</td>
    <td>datetime</td>
  </tr>
  <tr>
    <td>created_at</td>
    <td>datetime</td>
    <td>updated_at</td>
    <td>datetime</td>
  </tr>
  <tr>
    <td>updated_at</td>
    <td>datetime</td>
    <td></td>
    <td></td>
  </tr>
</table>

## Lab: Cafeteria 

### User Stories

- Version 1
  - As a user, I want to view a single ingredient
  - As a user, I want to view all ingredients
  - As a user, I want to create an ingredient with name and unit
  - As a user, I want to edit an ingredient's name and unit
  - As a user, I want to delete an ingredient

- Version 2
  - As a user, I want to view a single ingredient
  - As a user, I want to view all ingredients
  - As a user, I want to create an ingredient with name and unit
  - As a user, I want to edit an ingredient's name and unit
  - As a user, I want to delete an ingredient
  - As a user, I want to view a recipe
  - As a user, I want to view all recipes
  - As a user, I want to create a recipe with a name and description
  - As a user, I want to edit a recipe's name and description
  - As a user, I want to delete a recipe
  - As a user, I want to assign a single recipe to an ingredient
  - As a user, I want to assign multiple ingredients to a recipe
  
### Entity Relationship Diagrams

#### Version 1

<table>
  <th colspan="2" style="text-align:center">Ingredients</th>
  <tr>
    <td>id</td>
    <td>primary key</td>
  </tr>
  <tr>
    <td>name</td>
    <td>string</td>
  </tr>
  <tr>
    <td>unit</td>
    <td>string</td>
  </tr>
  <tr>
    <td>created_at</td>
    <td>datetime</td>
  </tr>
  <tr>
    <td>updated_at</td>
    <td>datetime</td>
  </tr>
</table>

#### Version 2

**Recipe** has many **Ingredients**

**Ingredients** belongs to **Recipe**

`Recipes` -|--< `Ingredients`

<table style="display:inline">
  <th colspan="2" style="text-align:center">Ingredients</th>
  <th colspan="2" style="text-align:center">
  Recipes
  </th>
  <tr>
    <td>id</td>
    <td>primary key</td>
    <td>id</td>
    <td>primary key</td>
  </tr>
  <tr>
    <td>name</td>
    <td>string</td>
    <td>name</td>
    <td>string</td>
  </tr>
  <tr>
    <td>unit</td>
    <td>string</td>
    <td>description</td>
    <td>string</td>
  </tr>
  <tr>
    <th>recipe_id</th>
    <th>foreign key</th>
    <td>created_at</td>
    <td>datetime</td>
  </tr>
  <tr>
    <td>created_at</td>
    <td>datetime</td>
    <td>updated_at</td>
    <td>datetime</td>
  </tr>
  <tr>
    <td>updated_at</td>
    <td>string</td>
    <td></td>
    <td></td>
  </tr>
</table>

## Tasks

Developers should run these often!

- `bin/rake routes` lists the endpoints available in your API.
- `bin/rake test` runs automated tests.
- `bin/rails console` opens a REPL that pre-loads the API.
- `bin/rails db` opens your database client and loads the correct database.
- `bin/rails server` starts the API.

## Additional Resources

- [Rails Association Basics](http://guides.rubyonrails.org/association_basics.html)
 Read the sections on belongs_to and has_many.
- [ActiveRecord Basics](http://guides.rubyonrails.org/active_record_basics.html)
- [ActiveRecord Migration Basics](http://guides.rubyonrails.org/active_record_migrations.html)
- [Rails Documentation](http://api.rubyonrails.org/)
- [Debugging Rails with the byebug Gem](http://guides.rubyonrails.org/debugging_rails_applications.html#debugging-with-the-byebug-gem)
- [With So Much Rails to Learn, Where Do You Start?](http://www.justinweiss.com/blog/2015/05/25/with-so-much-rails-to-learn/)
