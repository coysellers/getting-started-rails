# Getting Started with Rails

The notes below are simply for my personal use and career development. For the source of these notes visit the official [set-by-step guide](http://guides.rubyonrails.org/getting_started.html) to getting starting with Rails.

## Section Checklist

- [x] 1 Guide Assumptions
- [x] 2 What is Rails?
- [x] 3 Creating a New Rails Project
- [x] 4 Hello, Rails!
- [ ] 5 Getting Up and Running
- [ ] 6 Adding a Second Model
- [ ] 7 Refactoring
- [ ] 8 Deleting Comments
- [ ] 9 Security
- [ ] 10 What's Next?
- [ ] 11 Configuration Gotchas


## Setup

* Check Ruby version `$ ruby -v`
* Check sqlite3 version `$ sqlite3 --version`
* Install Rails globally `$ gem install rails`
* Verify Rails has been properly installed `$ rails --version`

### Creating Blog Application

Ruby comes packaged with scripts called `generators`.

Example: cd to project folder and run `$ rails new blog`.
* Then cd into the application to work in it `$ cd blog`.

### Server

In application folder, run `$ bin/rails server` then visit http://localhost:3000/.
* The "Yay! You're on Rails" screen should be displaying.

### Say "Hello"

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


### Getting Up and Running

Creating a _resource_.

A _resource_ is a collection of similar objects like:
* articles
* people
* animals

> CRUD operations can be used on items in a resources (CRUD - create, read, update and destroy)

Rails provides a _resources_ method that declares a standard _REST_ resource.


### Laying Down the Ground Work

> A controller is simply a class that is defined to inherit from _ApplicationController_

Run `$ bin/rails generate controller Articles`

```
class ArticlesController < ApplicationController
end
```

`/articles/new.html.erb`
* `.html` is the format
* `.erb` is the handler


### Common Commands

| Command | What it does |
| --- | :---:|
| $ ruby -v | checks Ruby version |
| $ sqlite3 --version | Checks sqlite3 version |
| $ gem install rails | Install Rails |
| $ rails --version | Checks Rails version |
| $ rails new `application-name` | Generates new Application |
| $ bin/rails routes | Shows routes for all RESTful actions |
