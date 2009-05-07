Roleify
=======

A Rails authorization plugin

Dependent on Clearance (should be configurable in the future though)

Example
=======

Make sure your User object has a "role" attribute (String).

Add an initializer
------------------

Roleify::Role.configure("role_a", "role_b") do
  {
    :role_a => { :issues =>  :all },
    :role_b => { :issues => "index" }
  }
end

In the example above "role_a" and "role_b" are the roles you are defining. The block contains the rules for these roles. There is no need to define an "admin" role, since it's added by default.

* Users with role "role_a" are allowed to access all of IssuesController actions.
* Users with role "role_b" are only allowed to access the index action of the IssuesController.
* Users with role "admin" are allowed to access all actions of all controllers.

The controller
--------------

class IssuesController < ActionController::Base
  include Clearance::Authentication
  include Roleify::RoleifyableController
end

The User model
--------------

class User < ActiveRecord::Base
  include Clearance::User
  include Roleify::RoleifyableModel
end

Extra's
=======

Constants: Roleify::Role::ADMIN, Roleify::Role::ROLE_A, Roleify::Role::ROLE_B

Named scopes are automatically added: User.admins, User.role_as, User.role_bs



Copyright (c) 2009 Koen Van der Auwera - 10to1, released under the MIT license