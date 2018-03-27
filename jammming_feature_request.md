# Feature Request
Enter to Search & Album Art
March 8, 2018

## OBJECTIVE
Allow users to hit enter to search for tracks and add album art to the tracks that are returned.

## BACKGROUND 
The only way to search for a track at the moment is to click the search button. It is a common user experience to be able to hit the enter key to return search queries. When looking for songs, it is also common to see the album art of a track.

- Ability for user to hit enter key to search for a track name
- Ability to see the album cover of each track that is searched for

## TECHNICAL DESIGN
This part will be broken up into two sections: the search functionality and the album cover.

### Search Functionality
This functionality involves modifying the `SearchBar.js` file. We had to add a listener for whenever the user types something to the <input> tag that will handle key presses. It will look something like `onKeyPress={this.handleKeyPress}`. 

For the function to actually handle the key press (HandleKeyPress) it will accept an event and check if it is equal to the enter key. If it is, then it should call the search function.

### Album Cover
This functionality involves modifying the `Spotify.js` and `Track.js` files.

Within `Spotify.js`, the search function needed to be updated to get information on the album cover. This can be done with `track.album.images[2].url` and set to a new property to map over within the jsonResponse.

Once the image can be captured from the spotify API, we need to render it on the front-end. Within the tracks render function, an image tag needs to be set to the album cover. In this case, it would look something like this: <img src={this.props.track.albumCover} />. The alt tag is generally optional, but react throws a warning. This can be solved by putting the name of the album within the alt tag, like so: `alt={this.props.track.album}`.

## CAVEATS

There are not many drawbacks to the proposed solutions. 

The search functionality is standard, and introduces minimal code.

A possible alternative to the album art rendering is that this image returned may be raw, and possibly uncompressed. Adding middleware to handle image compression or a gulp task to ensure that these images are optimized when the are rendered on the front-end will help performance, especially if the user ever wanted to view say 50 or 100 results at a time on mobile devices.
