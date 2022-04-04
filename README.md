API: Spotify
What does it do: Returns JSON metadata about music artists, albums, and tracks, directly from their DB.

For example, we can get all the information about a certain artist.

```
Route::get(/spotify/artists/{id}, function($id) {

    $response = Cache::remember("spotify-artists-id", 60, function () use ($id) {
        return Http::get("https://api.spotify.com/v1/artists/$id.json")->object();
    });

     return view('api.spotify', [
        'response' => $response,
    ]);
}

```

Any application can request data from Spotify Web API endpoints and many endpoints are open and will return data without requiring registration. However, if your application seeks access to a user’s personal data (profile, playlists, etc.) it must be registered. 

To register your application, go to your account dashboard here:
https://developer.spotify.com/dashboard/

Click create an app:
<img src = "https://developer.spotify.com/assets/createappdialog.png">

Enter an App Name and App Description of your choice (they will be displayed to the user on the grant screen), put a tick in the Developer Terms of Service checkbox and finally click on CREATE. Your application is now registered, and you’ll be redirected to the app overview page.

You will get access to:
```
<li>
    <ul>App metrics, such as daily and monthly active users or number of users per country. Note that the metrics are initially empty.
    </ul>
<ul>
    App Status. By default, your app will be in Development Mode with limits on the number of users who can install it, and the number of API requests it can make. Note that you can request an extension of this quota if needed by clicking on the Request Extension link.
</ul>
<ul>App settings. </ul>
<ul> Client ID, the unique identifier of your app. </ul>
<ul>Client Secret, the key you will use to authorize your Web API or SDK calls. </ul>
</li>
```

Example JSON Response:
<img src = "https://gyazo.com/3469174d908646d82de5cb2c31fd677c">