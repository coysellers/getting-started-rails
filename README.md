# Getting Started with Rails

The notes below are simply for my personal use and career development. For the source of these notes visit the official [set-by-step guide](http://guides.rubyonrails.org/getting_started.html) to getting starting with Rails.




## Section Checklist

- [x] 1 Guide Assumptions
- [x] 2 What is Rails?
- [x] 3 Creating a New Rails Project
    - [x] 3.1 Installing Rails
    - [x] 3.2 Creating the Blog Application
- [x] 4 Hello, Rails!
    - [x] 4.1 Starting up the Web Server
    - [x] 4.2 Say "Hello", Rails
    - [x] 4.3 Setting the Application Home Page
- [ ] 5 Getting Up and Running
    - [x] 5.1 Laying down the groundwork
    - [x] 5.2 The first form
    - [x] 5.3 Creating articles
    - [x] 5.4 Creating the Article model
    - [ ] 5.5 Running a Migration
    - [ ] 5.6 Saving data in the controller
    - [ ] 5.7 Showing Articles
    - [ ] 5.8 Listing all articles
    - [ ] 5.9 Adding links
    - [ ] 5.10 Adding Some Validation
    - [ ] 5.11 Updating Articles
    - [ ] 5.12 Using partials to clean up duplication in views
    - [ ] 5.13 Deleting Articles
- [ ] 6 Adding a Second Model
    - [ ] 6.1 Generating a Model
    - [ ] 6.2 Associating Models
    - [ ] 6.3 Adding a Route for Comments
    - [ ] 6.4 Generating a Controller
- [ ] 7 Refactoring
    - [ ] 7.1 Rendering Partial Collections
    - [ ] 7.2 Rendering a Partial Form
- [ ] 8 Deleting Comments
    - [ ] 8.1 Deleting Associated Objects
- [ ] 9 Security
    - [ ] 9.1 Basic Authentication
    - [ ] 9.2 Other Security Considerations
- [ ] 10 What's Next?
- [ ] 11 Configuration Gotchas


## 1 Guide Assumptions

Resources:
* [Ruby Language](https://www.ruby-lang.org/en/documentation/)


## 2 What is Rails?

Rails is a web application framework running on the Ruby programming language.

Two major guiding principles:
* DRY
* Convention over Configuration


## 3 Creating a New Rails Project

### 3.1 Installing Rails
* Check Ruby version `$ ruby -v`
* Check sqlite3 version `$ sqlite3 --version`
* Install Rails globally `$ gem install rails`
* Verify Rails has been properly installed `$ rails --version`

### 3.2 Creating Blog Application
Ruby comes packaged with scripts called `generators`.

Example: cd to project folder and run `$ rails new blog`.
* Then cd into the application to work in it `$ cd blog`.

## Hello, Rails!

### 4.1 Starting up the Web Server
In application folder, run `$ bin/rails server` then visit http://localhost:3000/.
* The "Yay! You're on Rails" screen should be displaying.

### 4.2 Say "Hello", Rails
Minimum requirements:
* controller
* view

The `controller` recieves requests for the app and a `view's` purpose is to display the information.
* By default, view templates are written in `eRuby` (Embedded Ruby).

To Create a new `controller`, cd into the application folder and run `$ bin/rails generate controller Welcome index`
* `Welcome` is the new controller and the action is `index`.

For this instance the controller is located at `app/controllers/welcome_controller.rb` and the view is located at `app/views/welcome/index.html.erb`.

Remove contents of the `index.html.erb` and replace with `<h1>Hello, Rails!</h1>`.

Modify the `config/routes.rb` file by adding `root 'welcome#index'`.

```
Rails.application.routes.draw do
    get 'welcome/index'
    
    root 'welcome#index'
end
```


## 5 Getting Up and Running

Creating a _resource_.

A _resource_ is a collection of similar objects like:
* articles
* people
* animals

> CRUD operations can be used on items in a resources (CRUD - create, read, update and destroy)

Rails provides a _resources_ method that declares a standard _REST_ resource.


### 5.1 Laying Down the Ground Work
> A controller is simply a class that is defined to inherit from _ApplicationController_

Run `$ bin/rails generate controller Articles`

```
class ArticlesController < ApplicationController
end
```
There are __public__, __private__, and __protected__ methods in Ruby
* only __public__ methods can be actions for __controllers__

`/articles/new.html.erb`
* `.html` is the format
* `.erb` is the handler


### 5.2 The first form
The __form builder__ is provided by a helper method called `form_with`.

Example Form located here `app/views/articles/new.html.erb`:
```
<%= form_with scope: :article, url: articles_path, local: true do |form| %>
    <p>
        <%= form.label :title %><br>
        <%= form.text_field :title %>
    </p>
    
    <p>
        <%= form.label :text %><br>
        <%= form.text_area :text %>
    </p>
    
    <p>
        <%= form.submit %>
    </p>
<% end %>
```
* The helper `form_with` called and passed an indetifiying scope for the form.
    * The symbol `:article` is the scope and tells the helper what this form is for.
* The `FormBuilder` object _(represented by `form`)_ is being used for the two `label`, two `text`, and `submit` fields.
* By default the `action` attribute points to the current page, _/articles/new)_.
    * The form needs a different `URL` - `url: articles_path`
    * In this form the `articles_path` helper is passed to the `:url` option. - `url: articles_path`


### 5.3 Creating articles
* Make a `create` actions within the `ArticlesController` class in _app/controllers/articles_controller.rb_.
* When submitted the form feilds are sent as _parameters_. Reference these params using the `render` method.
* Add a key value pair
    * key - `plain:`
    * value - `params[:article].inspect`

Render and define params:
```
class ArticlesController < ApplicationController
    def new
    end

    def create
        render plain: params[:article].inspect
    end
end
```

Returned params on submit:
```
<ActionController::Parameters {"title"=>"First Article!", "text"=>"This is my first article."} permitted: false>
```


### 5.4 Creating the Article model

Model Generator command:
`$ bin/rails generate model Article title:string text:text`

> This generates a model called `Article` with a _title_ attribute set to a _string_ type and a _text_ attribute set to _text_ type. The attributes are added to the database in the `articles` table and mapped to the `Article` model.

Files created:
1. app/models/article.rb
2. db/migrate/20180302135637_create_articles.rb
3. blog/test/fixtures/articles.yml
4. blog/test/models/article_test.rb

> Active Record is used and automatically maps the column names to model attributes.


### Common Commands

| Command | What it does |
| --- | :---:|
| $ ruby -v | checks Ruby version |
| $ sqlite3 --version | Checks sqlite3 version |
| $ gem install rails | Install Rails |
| $ rails --version | Checks Rails version |
| $ rails new `application-name` | Generates new Application |
| $ bin/rails routes | Shows routes for all RESTful actions |
