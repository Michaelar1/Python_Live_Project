# Python LiveProject
  For two weeks toward the end of my tenure with The Tech Academy Software Development Bootcamp, I worked on a Live Project to develop a fully-functional web app using Python/Django. I found that this was a wonderful opportunity to find my strengths, hone in on what I needed to practice more, and to learn to use newer programming features on the fly. I really enjoyed this process and it gave me a lot more perspective on what will be required to succeed in my development career. 
  
  In this project, I created a Danish Tourism Web App that utilizes a database and CRUD capabilities. Users can catalog tourist attractions in various cities, view the locations, edit location information, and delete locations. The user can also find the top tour companies and search for flights to Denmark and the Faroe Islands.
  
  I worked on both Front-End and Back-End to develop this app, in the process learning more about web-scraping and working with APIs. Personally, I was par During the course of this two-week sprint, I also became much more familiar with Agile and Scrum project management methodologies, including daily Stand Up meetings and weekly Code Retrospectives. 
  
  Below, I have detailed the stories I worked on with code snippets and gifs to allow you to see the finished project.
  
  ## Setting Up the Home Page and the Database
  * [Setting Up the Basic App](https://github.com/Michaelar1/Python_Live_Project/blob/main/README.md#setting-up-the-basic-app)
  * [Making Models]
  * [Displaying the Database]
  * [Creating the Details Page]
  
  ### Setting Up the Basic App
In this part of the project, I had to set up the base html code and home page, register URL patterns, and add some functionality and styling for the home page. In doing so, I set up the navbar and footer templates as well. My biggest challenge at this point was managing time versus my desire to make the styling perfect. However, I quickly learned to set better pacing for myself and perfected the look of my app toward the end of the project when I had more time.

![](https://github.com/Michaelar1/Python_Live_Project/blob/main/gif_views/Home_Page.gif)

    {% extends 'DanishTourism_base.html' %}

    {% block title %}Danish Tourism App{% endblock %}

    {% block header %}Welcome to the Danish Tourism App! &#9679; Velkommen til det Danske Turisme App!{% endblock %}

    {% block content %}
    <p>Do you dream of exploring Denmark? Let us help you make your dreams come true!</p>
    {% load static %}<img src="{% static 'images/dannebrog.jpg' %}" class="dt-home-img" alt="Danish Flag">
    <br>
    <button class="dt-home-tourLink btn"><a href="{% url 'DanishTourism_tourWidget' %}" class="dt-home-tourLink">View Available Tours!</a></button>
    <button class="dt-home-flightLink btn"><a href="{% url 'DanishTourism_PlanTrip' %}" class="dt-home-flightLink">Plan Your Trip!</a></button>

    {% endblock %}
