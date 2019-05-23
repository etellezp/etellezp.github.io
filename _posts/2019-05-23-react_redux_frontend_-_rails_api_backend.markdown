---
layout: post
title:      "React / Redux frontend - Rails API backend "
date:       2019-05-23 18:13:30 +0000
permalink:  react_redux_frontend_-_rails_api_backend
---


The main purpose of the application is to be able to find personel for your event / party. You can see profiles of hosts, waiters, DJs, chefs, decorators, etc. After you find a profile that you are interested you can see comments (reviews and ratings) related to that profile.

To keep things simple I created two repositories, one for the backend and one for the frontend. The backend was generated with the rails new --api parameter and the frontend was generated with the create-react-app library. 

In order to connect both applications you need to setup CORS in your rails backend using the gem 'rack-cors' and modifiying the cors.rb file located inside the initializers folder. 

```
 Rails.application.config.middleware.insert_before 0, Rack::Cors do
  allow do
    origins 'localhost:3000'

    resource '*',
      headers: :any,
      methods: [:get, :post, :put, :patch, :delete, :options, :head]
  end
end
```

This code inside the cors.rb file is what is letting the backend recieve resources from localhost:3000 (where your frontend is located) and allow you to do fetch requests from your frontend to the backend. 

The rest of the backend was pretty simple, just two models, profiles and comments. Where profiles has_many comments and comments belong_to a profile.

```
  ActiveRecord::Schema.define(version: 20190312153100) do

  # These are extensions that must be enabled in order to support this database
  enable_extension "plpgsql"

  create_table "comments", force: :cascade do |t|
    t.text "review"
    t.integer "rating"
    t.bigint "profile_id"
    t.datetime "created_at", null: false
    t.datetime "updated_at", null: false
    t.index ["profile_id"], name: "index_comments_on_profile_id"
  end

  create_table "profiles", force: :cascade do |t|
    t.string "image_url"
    t.text "about"
    t.integer "rate"
    t.string "location"
    t.string "name"
    t.string "skill"
    t.datetime "created_at", null: false
    t.datetime "updated_at", null: false
  end

  add_foreign_key "comments", "profiles"
end
```

Majority of the application was coded in the frontend and it was also the most complicated part because many components interact with each other, Redux was the state management and React Router was used for navigation. 
In order to keep things simple and organized I decided that index.js was going to be the file in charge of passing the Redux store and the React Router to the App component (which is the parent of every other component).

```
import React from 'react';
import ReactDOM from 'react-dom';
import { BrowserRouter } from 'react-router-dom';
import 'bootstrap/dist/css/bootstrap.min.css';
import App from './containers/App';
import * as serviceWorker from './serviceWorker';
import { Provider } from 'react-redux';
import thunk from 'redux-thunk';
import { createStore, applyMiddleware } from 'redux';
import rootReducer from './reducers';
import './index.css'

const store = createStore(rootReducer, applyMiddleware(thunk))

ReactDOM.render(
  <Provider store={ store }>
    <BrowserRouter>
      <App />
    </BrowserRouter>
  </Provider>,
  document.getElementById('root')
);
```

And the App component was going to be in charge of passing all the routes that render the rest of the components. That way all the components can interact between each other via links. 

```
class App extends Component {
  render() {
    return (
      <>
        <NavBar />
        <div>
          <Switch>
            <Route exact path="/" component={Home} />
            <Route exact path="/profiles" component={ProfilesList} />
            <Route path="/profiles/new" component={ProfileForm} />
            <Route exact path="/profiles/:id" component={Profile} />
            <Route path="/profiles/:id/edit" component={EditProfile} />
            <Route exact path="/profiles/:id/comments/new" component={CommentForm} />
          </Switch>
        </div>

        <Particles className="particles" params={particlesOptions}/>
      </>
    )
  }
}

export default App;

```

Once those files were set up, the next part of the organization was to keep components that interact with the state in a container folder and keep the component that just present the data to the DOM in a presentational component folder. 
Also the actions and the reducers had their own folder, that way the code was organized making it easier to debug and to add more functionality. 

You can see the backend code at [https://github.com/etellezp/event-jobs-api](http://)<br>
You can see the frontend code at [https://github.com/etellezp/event-jobs-client](http://)

After graduation I will work on adding Users to the application and also adding the functionality to be able to contact a profile. 

