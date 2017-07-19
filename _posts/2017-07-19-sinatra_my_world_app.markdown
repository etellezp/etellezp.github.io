---
layout: post
title:  "Sinatra My_World App"
date:   2017-07-19 15:38:40 +0000
---


Today I finished my Sinatra CRUD App ! 
Since I was a little kid I have always enjoyed traveling, meeting new people, learning from new cultures and realizing that this small world have beautiful places all over it. 
Nowadays when I travel I always use two main applications. The first one is Airbnb(I rather stay with a local that will teach me more about their culture and living than staying in a hotel), the second one is TripAdvisor. When I am lost TripAdvisor is my way to go, and the reviews has never failed me. 
That is why I wanted to created something similar to TripAdvisor (of course not that complex and way much simpler). 
My app My_World consists in two models: Traveler and Recommendation. Traveler has_many recommendations and Recommendation belong_to a traveler. 

My recommendations for the project would be the following:

1. The most difficult part of the project is to start. Having an empty IDE can be very intimidating and you always ask the question: Where do I start? or What should I do? In order to avoid this first problem use the Corneal Sinatra Gem. It will automatically set up all your files for you, that way you can only focus on code and not setting up your files. 
2. Start with your database and associations. Do not rush in this part, this is the base of your building, if you do not make your associations and database the right way everything is going to fall down. Once you have your database, migrations and associations ready play with them using the Tux gem. That way you are 100% sure that your associations are working the way you wanted to.
3. Divide the controllers into files. Do not have all your controllers in the application_controller, your code will get messy quickly and will be very hard to debug. In my case I had a file for application_controller, one for travelers_controller and another one for recommendations_controller. Easier to read, easier to debug, easier to code. 
4. DO NOT FORGET to mount your controllers in the config.ru file. Nothing will work if you forget this step. 
5. If you are having problems in your controllers remember CRUD (create, read, update, delete).
6. Lastly, start working in your views. Use shotgun to see how your application is coming along and constantly use binding.pry to make sure the information you are passing from your controllers to your views is the correct one. 

If you want to take a look at my Sinatra Application this is the link https://github.com/etellezp/my_world
You can also direct message me in Slack @etellezp

Now to start a new journey with Rails!!
