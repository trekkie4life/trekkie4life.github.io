---
layout: post
title: "Phase 2: Week 2: Day 2 - JavaScript Racer"
date: 2014-02-25 13:28:49 -0800
comments: true
categories: 
---


**8:00 - Arrive**

##~~Ruby~~ JavaScript Racer

Given a very basic HTML template, utilize JS to map out actions to events (in this case, keyboard presses) to then animate things in the view.

In the case of the keyboard, we only the action of only two keys - 'P' for player 1, and 'Q' for player 2.  We also don't want someone to be able to cheat and merely hold down a key and have their "racer" zoom across the screen at lightening speed. So we want `.keyup` which will act when a key is released. Perfecto.

We also need to change the position of our 'racer' upon each key press. Here, we make use of the HTML template, and add a class to the sibling of the currently active cell. then we remove that class from the previous spot.


```javascript
var player1Movement = function () {
  $(document).keyup(function(e) {
    if (e.keyCode == 80 && !game_end()){
      $("#player1_strip .active").next().addClass("active");
      $("#player1_strip .active").prev().removeClass("active");
    }
  });
}
```

How do we know we are done? When the active cell is also the final cell in racetrack.

just check out line 2 in this code

```javascript
var game_end = function () {
  if ($("#player1_strip .active").hasClass("end") == true){
    $(".game_status").html("PLAYER 1 WINS!");
    $("#restart").css("display", "block");
    $("#fuck_yeah").css("display", "block");
    return true;
  } else if ($("#player2_strip .active").hasClass("end") == true){
    $(".game_status").html("PLAYER 2 WINS!");
    $("#restart").css("display", "block");
    $("#fuck_yeah").css("display", "block");
    return true;
  } else {
    return false;
  }
}
```

When the game finishes, we want to acknowledge that it finishes and then have a rematch button pop up.

The rematch button, we actually already have in the page.

Here's a snippet from the HTML file

```html
<body>
  <h1 class="game_status"></h1>
  <button type="button" id="restart">Rematch!</button>
```

So to hide it, we just use CSS

```css
#restart { display: none; }
```

How do we show it? If you paid extra special attention to how our game ends, you can pat yourself on the back. For everyone else, we use jQuery and capture the `#restart` id and then change the CSS method and use to change the property value.

```javascript
var game_end = function () {
  if ($("#player1_strip .active").hasClass("end") == true){
    $(".game_status").html("PLAYER 1 WINS!");
    $("#restart").css("display", "block");
```

##JavaScript Racer - MVC

We did this in the afternoon and used our Sinatra skeleton to get it to work.

We make a page to have our players enter their name - we provide a default in the case that a name isn't entered.



```ruby app/controllers/index.rb
post '/new_game' do
  params[:username1] == "" ? player1 = "Your mom"  : player1= params[:username1]
  params[:username2] == "" ? player2 = "Chuck Norris"  : player2= params[:username2]
```

Then we query the database to find or create a player of that name `User.find_or_create_by_username(player1)`. Then we add those values to the session to hold onto those User ID's so we can later write them to the database

```ruby app/controllers/index.rb
  @player1 = User.find_or_create_by_username(player1)
  @player2 = User.find_or_create_by_username(player2)
  session[:player1_id] = @player1.id
  session[:player2_id] = @player2.id
```
It's time to start the game, we pass in the player_ids to the URL, as a way of saving which users are playing the game.

```ruby app/controllers/index.rb
  redirect "/play_game/player1_id=#{@player1.id}/player2_id=#{@player2.id}"
end
```


**11:00pm - Depart**

>I, myself, have had many failures and I've learned that if you are not failing a lot, you are probably not being as creative as you could be - you aren't stretching your imagination.  
- J. Backus

