---
layout: post
title: Kele API Client
feature-img: "img/catoncomputerhamster_Fotor.jpg"
thumbnail-path: "img/catoncomputerhamster.jpg"
short-description: Kele is a Ruby Gem API client used to access the Bloc API.

---

## Summary
Kele is a Ruby Gem API client used to access the Bloc API.

## Explanation
For this assignment we were instructed to create a gem that interacted with BLOCs student endpoints.

## Problem
This project was so completely different from my other projects I thought I would never get through it. From the very first checkpoint I was like "wha???"

## Solution
This was really whenever I got each step to work. Call up my student information? Check! Call up my Mentor's availability? Check! Retrieve a list of my messages, respond to an existing message, create a new message thread, and submit checkpoint assignments? Check, Check, Check and Check!

## Results

#### Here are a few images from the final product.

{:.center}
Since there are no website images to capture, I'll just include some of my code here.  Here is the main bulk of code that grabs my own info from BLOC, my mentor avalability, retrieves and creates messages, and lastly creates a submission:

{% highlight ruby %}
require 'httparty'
require 'roadmap'

class Kele
  include HTTParty
  include RoadMap

  def initialize(email, password)
     response = self.class.post("https://www.bloc.io/api/v1/sessions", body: {email: email, password: password})
     raise "invalid email/pass" if response.code != 200
     @auth_token = response["auth_token"]
  end

  def get_me
    url = "https://www.bloc.io/api/v1/users/me"
    response = self.class.get(url, headers: { "authorization" => @auth_token })
    JSON.parse(response.body)
  end

  def get_mentor_availability(mentor_id)
    url = "https://www.bloc.io/api/v1/mentors/#{mentor_id}/student_availability"
    response = self.class.get(url, headers: { "authorization" => @auth_token })
    h = JSON.parse(response.body)
    h.to_a
  end

  def get_messages(number = nil)
    url = "https://www.bloc.io/api/v1/message_threads/"
    body = {page: number}
    if number
      response = self.class.get(url, headers: { "authorization" => @auth_token }, body: body)
    else
      response = self.class.get(url, headers: { "authorization" => @auth_token })
    end
    JSON.parse(response.body)
  end

  def create_messages(string, text)
    url = "https://www.bloc.io/api/v1/messages"
    body = {
      user_id: get_me["id"],
      recipient_id: "539470",
      subject: string,
      "stripped-text"=> text
    }
    response = self.class.post(url, headers: { "authorization" => @auth_token }, body: body)
    JSON.parse(response.body)
  end

  def create_submission(checkpoint_id, assignment_branch, assignment_commit_link, comment)
    url = "https://www.bloc.io/api/v1/checkpoint_submissions"
    body = {
      checkpoint_id: checkpoint_id,
      assignment_branch: assignment_branch,
      assignment_commit_link: assignment_commit_link,
      comment: comment,
      enrollment_id: get_me["current_enrollment"]["id"]
    }
    response = self.class.post(url, headers: { "authorization" => @auth_token }, body: body)
    JSON.parse(response.body)
  end

end
{% endhighlight %}

***

## Conclusion
This project started off being really hard because it was so different from any other project I worked on and was different from anything I learned in the sense that there were no controllers, models or views to think about. For each checkpoint here I kept coming SUPER close but then would need a bit of guiddance from my mentor to help me debug. By the end I really felt like I understood it though and it was neat to say I created a gem (even though BLOC really told me how to create it.) Just working through this though gave me a better understanding of how it works and I know that will help me in the real world.
