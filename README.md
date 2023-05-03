# Python LiveProject
  For two weeks toward the end of my tenure with The Tech Academy Software Development Bootcamp, I worked on a Live Project to develop a fully-functional web app using Python/Django. I found that this was a wonderful opportunity to find my strengths, hone in on what I needed to practice more, and to learn to use newer programming features on the fly. I really enjoyed this process and it gave me a lot more perspective on what will be required to succeed in my development career. 
  
  In this project, I created a Danish Tourism Web App that utilizes a database and CRUD capabilities. Users can catalog tourist attractions in various cities, view the locations, edit location information, and delete locations. The user can also find the top tour companies and search for flights to Denmark and the Faroe Islands.
  
  I worked on both Front-End and Back-End to develop this app, in the process learning more about web-scraping and working with APIs. During the course of this two-week sprint, I also became much more familiar with Agile and Scrum project management methodologies, including daily Stand Up meetings and weekly Code Retrospectives. 
  
  Below, I have detailed the stories I worked on with code snippets and gifs to allow you to see the finished project.
  
  ## Setting Up the Home Page and the Database
  * [Setting Up the Basic App](https://github.com/Michaelar1/Python_Live_Project/blob/main/README.md#setting-up-the-basic-app)
  * [Making Models](https://github.com/Michaelar1/Python_Live_Project/blob/main/README.md#making-models)
  * [Displaying the Database](https://github.com/Michaelar1/Python_Live_Project/blob/main/README.md#displaying-the-database)
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
    

### Making Models
This part of the project was simply to make the model for the input form and to get the Add Location page to render. I used a function in views.py to render the page using the model I created in models.py and added additional styling to make my page look more user-friendly and generally pleasant to look at.

![](https://github.com/Michaelar1/Python_Live_Project/blob/main/gif_views/Add_Location.gif)

    class Location(models.Model):
      type = models.CharField(max_length=60, choices=TYPE_CHOICES)
      name = models.CharField(max_length=60, default="", blank=True, null=False)
      city = models.CharField(max_length=60, choices=CITY_CHOICES)
      description = models.TextField(max_length=350, default="", blank=True)
      image = models.CharField(max_length=1000, default="http://...")

      Locations = models.Manager()

      def __str__(self):
         return self.name


    # This function will render the Add Location page when requested
    def add_location(request):
        # Retrieves the Location form
        form = LocationForm(data=request.POST or None, )
        # Checks if request method is POST
        if request.method == 'POST':
            if form.is_valid():  # Checks to see if the submitted form is valid
                form.save()  # Saves the new location
                return redirect('DanishTourism_Locations')  # Returns to location page
        content = {'form': form}  # Saves content to the template as a dictionary
        # Adds content of form to page
        return render(request, 'DanishTourism_AddLocation.html', content)
        
### Displaying the Database
In this story, I created a Locations page that would display all items in the database. I added a function in views.py that would display the locations and used an HTML table and Django for loop to organize and display the locations. I would ideally have liked to add a filter function to this template, but was ultimately unable to due to the fact that the research I did on adding filters conflicted with the main app. I would love to do more research on this to be able to add a filter, as it would absolutely make my page more user-friendly.

![](https://github.com/Michaelar1/Python_Live_Project/blob/main/gif_views/Locations.gif)

    def displayLocations(request):
      locations = Location.Locations.all()
      content = {'locations': locations}
      return render(request, 'DanishTourism_Locations.html', content)
      
    <table class="dt-locations-table">
      <!-- Replace these with the Django-populated info -->
      <tr id="dt-locations-headerRow">
          <th>City</th>
          <th>Location</th>
          <th>Type</th>
          <th>Description</th>
          <th>View</th>
      </tr>
      {% for l in locations %}
      <tr>
          <td class="dt-locations-tdName"><a href="{% url 'DanishTourism_ViewDetails' l.pk %}">{{ l.name }}</a></td>
          <td>{{ l.city }}</td>
          <td>{{ l.type }}</td>
          <td>{{ l.description }}</td>
          <td><img src="{{ l.image }}" alt="{{ l.name }}"></td>
      </tr>
       {% endfor %}
    </table>
    
