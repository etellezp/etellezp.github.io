---
layout: post
title:      "Rails JS Project"
date:       2019-02-19 18:20:57 +0000
permalink:  rails_js_project
---


For my Rails JS project I decided to add the JavaScript and JSON API requirements to my old Rails project. I am passionate about scuba diving so for my old project I decided to create an app that can show dive sites and records associated to a particular dive site. Users can also create their own dive sites and records and see other users records. 

The Rails JS project was challenging because you had to change the structure of your application so now the interaction between the user and the app is made via JavaScript. It is important to take your time and pay close attention to where your files are located and which file is responsible for certain actions. Your code might be perfect, but a simple mistake in the order of the files in the asset pipeline and your app will not work. 

On of the goals of this project is to use JavaScript so you will only change the parts of the app that you want to change and avoid doing a reload of the app. This will increase the performance and the speed of your app because the app does not need to reload. In order to accomplish that you need to manipulate the links and stop making them work the way they are suppose to work. Hijacking the click event will be your best friend, using `e.preventDefault()` will stop the click event to do a reload of the page. Once you hijack the click event you will use the fetch API or AJAX to get a JSON data from your database, iterate thru that data and change the DOM with the formatting and data that you want.

I found challenging how to format the data that I was getting from the API and append it to the DOM. For that I found out that you can use the JS class constructor function and then use the prototype of that class to return HTML. 

For example:

Class Constructor:

```
function Site(site) {
  this.id = site.id
  this.name = site.name
  this.location = site.location
  this.records = site.records
}
```

Prototype returning HTML:

```
Site.prototype.formatSiteIndex = function() {
  let siteHtml = `
    <ul>
      <li>Name: <a href="/sites/${this.id}" data-id="${this.id}" class="js-site-link"><strong>${this.name}</strong></a></li>
      <li>Location: <strong>${this.location}</strong></li>
    </ul>
    <hr>
  `
  return siteHtml
}
```


Hijack click event, iterate thru the data and append the new format to the DOM:

```
const siteClickEvents = () => {
  $(".js-sites-button").on("click", (e) => {
    e.preventDefault()      # Hijack the click event
    fetch(`/sites.json`)     # get data thru the API
      .then(res => res.json())
      .then(data => {
        $(".js-load-sites").html('')
        data.forEach(site => {    #Iterate thru the data
          let newSite = new Site(site)
          let siteHtml = newSite.formatSiteIndex() #New format 
          $(".js-load-sites").append(siteHtml) #Add to the DOM
        })
      })
  })
```



