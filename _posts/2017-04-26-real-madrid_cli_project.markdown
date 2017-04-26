---
layout: post
title:  "Real-Madrid CLI Project"
date:   2017-04-26 15:39:31 +0000
---

Today I finished my CLI Project and I couldn't be more excited, another step towards my programming career. 

My CLI Project was about the Real Madrid Football (Soccer) Club. Real Madrid is the most successful football team in history and is also my favorite football team since I was a little kid. 

My project consisted of showing the user the list of the current 24 players that represent Real Madrid and then if the user wanted to know more information about an specific player they would be able to see that information in their browser. 

For example:

When the user type "list" the terminal will show the following:

1. Keylor Navas - Goalkeeper - 1
2. K. Casilla - Goalkeeper - 13
.
.
.
24. Morata - Forward - 21

All the way to 24. The first part is the name of the player, the second part is the position of the player and the last part is the jersey number of the player. 

I obtain that information by scrapping the following website [Real Madrid Squad](http://realmadrid.com/en/football/squad)

After the list is shown to the user if the user wanted to know more about a specific player it could type the list number and the browser will pop up with the player specific website. 
```
system("open '#{@squad.players[input.to_i-1].url}'")
```

That's the code to be able to make your terminal open a website with the url of your choice. 
If for example the user wanted to know more about the player morata, the user would type 24 and this website will open [Morata Real Madrid Player](http://http://www.realmadrid.com/en/football/squad/alvaro-borja-morata-martin)

I was able to learn a ton from this project, but the one thing I am never going to forget is the feeling of having an empty/blank IDE. This is the first time in the curriculum that we have to create something of our own. There are no instructions you have to follow, no TDD that shows you if you pass the test or not, no "Learn Open" or "Learn Submit" It really give you a lot of anxiety having a blank IDE with no idea of how to start. 

I recommend first looking for something that you really like, hobbies are a really good place to start working for your project. 
Also before you decide your project look at the website or websites that you are going to scrape, sometimes the websites are full of tables and makes it really complicated to scrape. If the website is simple to scrape your project will become way much simpler and it will take you less time. 
And very important do not forget the power of 'bundle' instead of creating folders and files and then dealing with dependencies, use the command "bundle gem your-cli-name" and it will help you big time with the setup of your environment. 

The hardest part is definitely to start, once you're coding it all becomes easier. 



