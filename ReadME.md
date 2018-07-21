# List of places App

## Description:
This App should let the user to search for a varity of places and to be able to view them on a map and also to view links to an articles written in NYTimes for the chosen area.

## This App uses a varity of libraries and API's:
### Libraries:
1- **Knockoutjs** - is a JavaScript library that helps you to create rich, responsive display and editor user interfaces with a clean underlying data model. Any time you have sections of UI that update dynamically (e.g., changing depending on the user’s actions or when an external data source changes), KO can help you implement it more simply and maintainably.

2- **jQuery** -  is a fast, small, and feature-rich JavaScript library. It makes things like HTML document traversal and manipulation, event handling, animation, and Ajax much simpler with an easy-to-use API that works across a multitude of browsers. With a combination of versatility and extensibility, jQuery has changed the way that millions of people write JavaScript.

### APIs:
1- **NYTimes** API to retrieve JSON data from NYTimes.
2- **Google Maps** to create our map , markers , infowindow and all the styles of this map.

## App Structure:
1- Open Index.html file
2- The app renders the template , Knockout binds the 'AppViewModel()' function to the view or template and make an asynchronous request to Google Maps API with a callback in 'initMap()' function.
3- When the app recieves the response in 'initMap()' it starts by initializing the needed Google Maps functions ex: 'google.maps.Marker()'.
4- The App initializes the rest of the functions ex: 'filterQueryResult()' , 'itemClick()' for the various functionality of the App.

## Files:

It consists of 3 main files **index.html** , **style.css** and **app.js**.

### index.html :

This file represents the view of the App , All what it do is presenting the data from the 'AppViewModel()'.

### style.css :

This file holds the styles of the elements or tags of the **index.html**.

### app.js :
This file holds all the functionality of the app , It holds the Data of the Model part 'locations[]' as well as the knockout binded function 'AppViewModel()' and also Google Maps callback function 'initMap()'.

Let's take an example of the functions that **app.js** holds:

''' 
this.itemClick= function(obj){
      var content = "Articles from NYTimes about this area : "+"<br>";
      var nytimesUrl = 'http://api.nytimes.com/svc/search/v2/articlesearch.json?q=' + obj.title + '&sort=newest&api-key=f8f7a03295ab4b4689050e7e60084855';
      $.ajax({
          url: nytimesUrl,
          success: function( response ) {
              var articles = response.response.docs;
              for (var i = 0; i < 5; i++) {
                  var article = articles[i];
                  content += i+1 +"- "+"<a href="+article.web_url+">"+article.snippet+"</a>"+"<br>";
              };
              infowindow.setContent(content);
          }
      }).fail(function() {
          infowindow.setContent("<p>Sorry,We couldn't get the articles from NYTimes!</p>");
      });
      infowindow.open(map, obj);
      // setting the bounce animation on the marker to null to avoid multiple bounce markers
      if (bounceHandler != obj) {
          bounceHandler.setAnimation(null);
          bounceHandler = obj;
          obj.setAnimation(google.maps.Animation.BOUNCE);
      }
  }
  '''
The 'itemClick()' function holds the functionality of the clicking event for both clicking the marker and clicking an item in the list , calls the NYTimes API asynchronously ( and ofcourse in handles the request failure) , seting the content of the infowindow (the popup window that presents the NYTimes articles) as well as creating the animation of the marker when it clicked.

## How to run this App ?
Simply by opening **index.html** file with any browser , and also make sure that your firewall doesn't block NYTimes or Google Maps services , if you are having any troubles with the blocking sevices in your operating system you can read this article : https://www.digitaltrends.com/computing/how-to-block-a-website/.