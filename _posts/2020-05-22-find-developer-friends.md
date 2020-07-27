---
title: "Use Twitter to find developer friends near you"
date: 2020-05-22 00:00:00
description: Using Twitter's advanced search and API we can find developers tweeting at any location and radius with geolocation data.
featured_image: "/images/Friends.jpeg"
---

![](/images/Friends.jpeg)

Being a developer can be tough, especially doing it all alone. That's why I always recommend surrounding yourself with like-minded 'Developer Friends' that support and motivate you.

Learn from each other, challenge each other, and work together to achieve the goals you set out. You'll not only learn about team dynamics but communication and collaboration. These are all important skills you'll need when working in a team as a developer.

So if you're looking to connect with like-minded individuals in your area then this trick is for you.

## I'm intrigued, go on.

Twitter has a really cool feature that not many people know about. You can search for tweets using geolocation data.

![Alt Twitter Geolocation Search](https://dev-to-uploads.s3.amazonaws.com/i/5pgyrkxqp5rxezj72vc3.png)

A lot of tweets are automatically tagged with geolocation data such a latitude, longitude, and radius ([skip ahead](#disable) if you want to disable this). Using Twitter's own search or API we can query for tweets using these fields:

```javascript
// The breakdown
geocode:latitude,longitude,radius
// Actual data
geocode:-36.8484597,174.7633315,10km
// Actual data with search terms included
geocode:40.7127753,-74.0059728,5mi "Coding" OR "Programming"
```

## Let's give it a try

Here we are searching for anyone tweeting related developer terms within a 5-mile radius of Facebook's Headquarters in California.

![Alt Twitter search for developers](https://dev-to-uploads.s3.amazonaws.com/i/gnyq4x0tze22shgwes3x.png)

## Now make it even easier

You're not going to want to keep Googling the coordinates and building your custom search strings each and every time. So I built a quick tool that does it all for you.

[Developer Friends](https://cyris.io/developerfriends/) will accept any address, location you can throw at it and it will automatically generate the coordinates and build your custom search query for you. Include the predefined search terms with the tickboxes or even add your own in the text box.
<br /><br />
<video width="100%" controls autoplay="true" loop="true">

  <source src="https://i.imgur.com/kigFdJ9.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>
<br />

After hitting search you'll be taken to Twitter with your own custom search query and everyone listed should be within the location and radius you specified. Now go make some developer friends. 👍

... <a name="disable"></a>

## I don't want to appear in these searches

No worries, you can disable geotagging on your tweets within Twitter's settings. You can read more about it [here](https://help.twitter.com/en/safety-and-security/tweet-location-settings)

---

I hope you'll be able to find, follow, and make plenty of developer friends. If you know any other cool tricks, let me know on Twitter [@sudo_overflow](https://twitter.com/sudo_overflow)
