---
layout: post
title: "Normalizing Data in Rails Forms for Beginners - Part 1"
date: 2013-03-09 13:23
comments: true
categories: [Ruby, Rails, Form Helpers]
---

My Flatiron School team, [Crystal](http://twitter.com/ACrystalC), [Tim](http://twitter.com/timspeaking) & [Tyler](http://twitter.com/TylerMDavis), and I recently presented our group project, [Jane's Lunch](http://janeslunch.com), at a [NYC on Rails MeetUp](http://www.meetup.com/nyc-on-rails/). Jane's Lunch is a web application that makes lunch delivery for group orders easy and fun.

I worked on a small piece of our Groups controller and some of the basic forms for creating and editing groups. This post is part one of two. In part one, I explain how I installed a timepicker for the group forms. In part two, I explain how I created a custom form helper to normalize the states input for user addresses.

<!-- more -->

##TimePicker
Our group form requires users to select a designated lunch time. We wanted to normalize the time data so that we wouldn't have problems parsing different time formats (e.g. "1:30PM" vs. "1:30 p.m." vs. "13:30"). A timepicker would solve this issue. I found [Bootstrap Timepicker](http://jdewit.github.com/bootstrap-timepicker/), a timepicker built by [@jdewit](https://github.com/jdewit/bootstrap-timepicker) for use with Twitter Bootstrap.

To install the gem, I added this line to our Gemfile:
    gem 'bootstrap-timepicker-rails'

Next, I added this line to install the CSS for Bootstrap Timepicker:
     *= require bootstrap-timepicker

Then, I added this line to link to the JavaScript file for Bootstrap Timepicker:
    //= require bootstrap-timepicker

For beginners, you'll want to include the entire line if you are installing the css and javascript. The code looks commented out, but Rails will actually implement that code even though it's commented out.

In the view for our group form, I added the following:

    <%= f.label(:lunch_time) %>
      <div class='input-append bootstrap-timepicker' style='display: inline;'>
        <input id='lunch_time' class='input-small' type='text' name='group[lunch_time]'>
        <span class='add-on'><i class='icon-time'></i></span>
      </div>

      <script type="text/javascript">
      $(document).ready(function(){
        $('#lunch_time').timepicker({
          template: 'dropdown',
          minuteStep: 15,
          showMeridian: false,
          showSeconds: false,
          defaultTime: '<%= @group.lunch_time || "12:00" %>'
        });
      });
      </script> 

Here's a breakdown to explain the block of code above:
![Timepicker Code ](/images/timepicker-step1.png "Bootstrap Timepicker Code Implementation Example")
Make sure to use an id not a class for the input selector that timepicker calls. I initially made lunch_time another class for the input instead of an id and it did not work.

![Timepicker Code ](/images/timepicker-step2.png "Bootstrap Timepicker Code Implementation Example")
I was wary of using an input form helper, so I just used regular HTML and mixed it in with the erb format. However, I wanted to make sure that my input name would be passed along with the rest of the group data in the params hash, so I used my browser inspector to check the name format for other inputs that used the rails form helpers. The names were set to 'group[attribute_name]' so that's the format I followed for the timepicker input.

![Timepicker Code ](/images/timepicker-step3.png "Bootstrap Timepicker Code Implementation Example")
My timepicker() call would not work without the document.ready.

![Timepicker Code ](/images/timepicker-step4.png "Bootstrap Timepicker Code Implementation Example")
I set the configurations for timepicker based on the [documentation](http://jdewit.github.com/bootstrap-timepicker/).

![Timepicker Code ](/images/timepicker-step5.png "Bootstrap Timepicker Code Implementation Example")
The timepicker is a little buggy if you do not set a defaultTime. In some cases, the timepicker will show NaN:NaN if you don't have any defaultTime set. 

If the defaultTime, is only set to "12:00", then the timepicker will always show "12:00," even if the user has already set a lunch time. 

The code fix above lets us set the timepicker to show the lunch time previously specified by the user or to show "12:00" if the user has not yet set it.

**Resources Links**

+ [Bootstrap Timepicker](http://jdewit.github.com/bootstrap-timepicker/): A TimePicker built for use with Twitter Bootstrap
+ [Gem](https://github.com/tispratik/bootstrap-timepicker-rails) for integrating Bootstrap Timepicker with Rails asset pipeline
+ Rails Guide for [Form Helpers](http://guides.rubyonrails.org/form_helpers.html)
+ I listened to this [Playlist](https://soundcloud.com/strangemachinemusic/sets/cool-2013) while writing this blog post.