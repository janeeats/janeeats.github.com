---
layout: post
title: "Normalizing Data in Rails Forms for Beginners - Part 2"
date: 2013-03-09 15:53
comments: true
categories: [Form Helpers, Ruby, Rails] 
---

This post, part two of two, explains some customizations I included in a basic form for creating and editing groups on my team's app, [Jane's Lunch](http://janeslunch.com). In my previous post, part one, I explain how I [installed a timepicker](/blog/2013/03/09/rails-form-helpers-for-beginners/) for the groups form. In this post, I explain how I created a custom form helper to normalize the states input for user addresses.

<!-- more -->

Jane's Lunch is built on the [Ordr.In API](https://hackfood.ordr.in/), which requires the two-letter, state abbreviation for delivery addresses. To ensure that the data we received from the group form would be clean and play well with the Ordr.In API, I used a custom form helper that would normalize the states input for group addresses. 

I put the following code in the group helper file:
    def us_states
    [
      ['Alabama', 'AL'],
      ['Alaska', 'AK'],
      ['Arizona', 'AZ'],
      ['Arkansas', 'AR'],
      ['California', 'CA'],
      ['Colorado', 'CO'],
      ['Connecticut', 'CT'],
      ['Delaware', 'DE'],
      ['District of Columbia', 'DC'],
      ['Florida', 'FL'],
      ['Georgia', 'GA'],
      ['Hawaii', 'HI'],
      ['Idaho', 'ID'],
      ['Illinois', 'IL'],
      ['Indiana', 'IN'],
      ['Iowa', 'IA'],
      ['Kansas', 'KS'],
      ['Kentucky', 'KY'],
      ['Louisiana', 'LA'],
      ['Maine', 'ME'],
      ['Maryland', 'MD'],
      ['Massachusetts', 'MA'],
      ['Michigan', 'MI'],
      ['Minnesota', 'MN'],
      ['Mississippi', 'MS'],
      ['Missouri', 'MO'],
      ['Montana', 'MT'],
      ['Nebraska', 'NE'],
      ['Nevada', 'NV'],
      ['New Hampshire', 'NH'],
      ['New Jersey', 'NJ'],
      ['New Mexico', 'NM'],
      ['New York', 'NY'],
      ['North Carolina', 'NC'],
      ['North Dakota', 'ND'],
      ['Ohio', 'OH'],
      ['Oklahoma', 'OK'],
      ['Oregon', 'OR'],
      ['Pennsylvania', 'PA'],
      ['Puerto Rico', 'PR'],
      ['Rhode Island', 'RI'],
      ['South Carolina', 'SC'],
      ['South Dakota', 'SD'],
      ['Tennessee', 'TN'],
      ['Texas', 'TX'],
      ['Utah', 'UT'],
      ['Vermont', 'VT'],
      ['Virginia', 'VA'],
      ['Washington', 'WA'],
      ['West Virginia', 'WV'],
      ['Wisconsin', 'WI'],
      ['Wyoming', 'WY']
    ]
    end

My group helper file is located in janeslunch/app/helpers/group_helper.rb.

Then in the view for the group form, I added this form helper to call the us_states helper:
    <%= f.label(:state) %>
    <%= f.select :state, us_states%>

On the frontend, the states are spelled out in the input dropdown:
![Form Helper Example ](/images/states-form-helper-frontend.jpg "States Form Helper Input Dropdown")

In the database, the states data is saved in the format that the Ordr.in API likes:
![Form Helper Example ](/images/states-form-helper-db.png "States Form Helper Helps us Normalize Data Inputs in our DB")

**Resources**

+ Help from StackOver flow for my [states select tag](http://stackoverflow.com/questions/6400010/rails-select-drop-down-for-states)
+ If you need select tags for other geographic locations, check out this handy gem [Carmen](https://github.com/jim/carmen) (and for [rails](https://github.com/jim/carmen-rails)).
+ Rails Guide for [Form Helpers](http://guides.rubyonrails.org/form_helpers.html)
+ Listened to this [playlist](https://soundcloud.com/charlotte-sky/sets/2013-remix) while writing this post.