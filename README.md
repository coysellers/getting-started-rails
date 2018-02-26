# Getting Started with Rails

The notes below are simply for my personal use and career development. For the source of these notes visit the official [set-by-step guide](http://guides.rubyonrails.org/getting_started.html) to getting starting with Rails.

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

Get Rails to say "Hello".

Minimum requirements:
* controller
* view

The `controller` recieves requests for the app and a `view's` purpose is to display the information.
* By default, view templates are written in `eRuby` (Embedded Ruby).

To Create a new `controller`, cd into the application folder and run `$ bin/rails generate controller Welcome index`
* `Welcome` is the new controller and the action is `index`.
