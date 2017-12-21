---
layout: post
title:      "Scuba Record, Rails Project"
date:       2017-12-20 23:42:20 -0500
permalink:  scuba_record_rails_project
---


Finally, after more than two weeks of non-stop bugs I finally finished my project. 
Scuba Diving is one of my many passions, I obtained my "open water" certification from PADI when I was 16; so for this rails project I decided to do something that relates with scuba diving. 
It is very common after each dive to record your experience/notes in a log/record, some records are interactive, others technical, and many more depending on your level of expertise. In my case I decided to give the user freedom to put in the notes of the record whatever they want regarding their dive. 

My app consists of three (3) models. User, Record and Site. 
```
class User < ApplicationRecord  
  has_many :records
  has_many :sites, through: :records
end
```

```
class Site < ApplicationRecord
  has_many :records
  has_many :users, through: :records
end
```

```
class Record < ApplicationRecord
  belongs_to :user, optional: true
  belongs_to :site
end
```

Even though coding your models is relatively easy, it was the hardest part of the project for me. I recommend taking your time while writing and setting up your models with a has_many through association. I decided to rush and because of that I lost an entire week dealing with bugs that were just caused because my associations were code incorrectly. 

One of the features that I am most proud of my application is that users can see other sites from other users and If they add a record to that site then the site will also belong to user and each user will be able to see both sites in their own sites index view. 

Thanks to the has_many through association I was able to accomplish this feature in the create action in records controller. 
```
  def create
    @record = Record.new(record_params)
    @record.site_id = @site.id
    @record.user_id = current_user.id
    if @record.save
      flash[:notice] = "Record was successfully created"
      redirect_to user_site_path(current_user, @site)
    else
      render 'new'
    end
  end
```

setting the @record.site_id = @site.id associates the record to the specific site, and @record.user_id = current_user.id associates the record to the user the is sign in. This was awesome but it gave me a bug that I was not able to figure out for three days. The bug was that it was duplicating the site instead of adding the records to the site. 
After three days of struggle I got help from a TA and we came with the solution that we needed to put the uniq method in the index action.

```
  def index
    @sites = Site.all
    if params[:user_id] && current_user
      @sites = current_user.sites.order("created_at DESC").uniq
    elsif params[:site_name]
      @sites = Site.search(params[:site_name])
    else
      @sites = Site.all.order("created_at DESC")
    end
  end
```

The reason we needed to add .uniq is because in rails 5.1+ the way I set up my code rails duplicates instead of adding, rails doesn't understand that associating records to a site in a user in a has_many through means that the user wants to add so it duplicates, the way to solve that is with .uniq that way it only show you 1 site with all the records belonging to that site. 

It was by far the toughest project but it was also the project that I learn the most. 

I think rails is fantastic and I can't wait to see what magic I can learn with javascript. 

You can check my entire code in the following link https://github.com/etellezp/ScubaRecords
you can contact me via slack at etellezp. 
