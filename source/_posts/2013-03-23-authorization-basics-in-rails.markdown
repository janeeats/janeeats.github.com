---
layout: post
title: "Authorization Basics in Rails"
date: 2013-03-23 17:27
comments: true
categories: [Authorization, Permissions, Ruby on Rails]
---

My new Flatiron School team, Anthony, Ei-lene, Eugene, and I are working on HandRaise, an application to handle student questions during lab or working sessions. HandRaise will help us keep track of which student questions are up next for teachers to answer. In this post, I explain how we implemented some basic authorization to allow or restrict specific users in taking certain actions.

<!-- more -->

**Authentication:** Before we assigned user permissions, we first implemented authentication so that users may sign in and sign out of the application. We followed the RailsCast tutorial, [Authentication from Scratch](http://railscasts.com/episodes/250-authentication-from-scratch-revised).

**Defining Permissions:** Once we had authentication running, we defined user roles. In our User model, we defined users roles as admins and students.

    class User < ActiveRecord::Base
      attr_accessible :role

      USER_ROLES = {
        :admin => 0,
        :student => 10
      }

Then we wrote instance methods in our User model that allowed us to define which users were admins and students.

    def set_as_admin 
      self.role = USER_ROLES[:admin]
    end

    def set_as_student 
      self.role = USER_ROLES[:student]
    end

**Authorization:** Next, we created methods to check if a user can edit the issue, destroy the issue, or mark the issue as resolved. We knew we wanted our authorization methods to read like English so that the other team members would be able to easily understand what is happening in the code. We wanted the following methods to work:

    def can_edit?(issue)
      true if owns?(issue) || admin?
    end

    def can_destroy?(issue)
      true if owns?(issue) || admin?
    end

    def can_resolve?(issue)
      true if owns?(issue) || admin?
    end

In order for the methods above to work, we had to create the methods admin? and owns?(issue). The admin? method checks if the user is an admin. The owns?(issue) method let's us pass an issue as an argument to see if the user created it.

    def owns?(issue)
      true if self.id == issue.user_id
    end

    def admin?
      true if self.role_name == :admin
    end

    def role_name
      User.user_roles.key(self.role)
    end

    def self.user_roles
      USER_ROLES
    end

After testing in the console to make sure our new methods worked, we added them to our view. The links to edit, resolve, or delete issues are only shown to users that are authorized to access those actions. Below is an example of how we used our new authorization methods in the view to check if a user has the ability to edit an issue:

    <% if @current_user.can_edit?(issue) %>
    <%= link_to 'Edit', edit_issue_path(issue) %>
    <% end %>

**Next Steps:** As you can see, we have some repetition in our authorization methods. The conditions for the can_edit?, can_resolve?, and can_delete? are all the same. Our next steps will include refactoring this code so we keep it dry.

**Resources:**

- Ryan Bates wrote an awesome authorization gem for Ruby on Rails called [CanCan](https://github.com/ryanb/cancan)
- RailsCast on how to implement [Authorization using CanCan](http://railscasts.com/episodes/192-authorization-with-cancan)
- Listened to this [mixtape by Diplo](https://soundcloud.com/diplo/diplo-friends-bbcr1xtra-march) for his Diplo & Friends radio show on BBC 1xtra. It's good.