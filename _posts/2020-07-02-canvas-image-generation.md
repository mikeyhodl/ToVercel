---
title: "Generating dynamic images on the fly for Email Marketing"
date: 2020-07-02 00:00:00
description: I was recently tasked to find a lightweight method to generate dynamic images on the fly for Email Campaigns. Sure we could use third-party solutions to do just that but for a fee. These are great services but being a developer I wanted to see if I could build my own that fits my needs.
featured_image: "/images/email.jpg"
---

![](/images/email.jpg)

I was recently tasked to find a lightweight method to generate dynamic images on the fly for Email Campaigns. Sure we could use third-party solutions to do just that but for a fee. These are great services but being a developer I wanted to see if I could build my own that fits my needs.

## But with a catch

A few rules I had set forward for myself.

- It needs to be lightweight
- No headless browsers
- No screenshot tools
- No saving and serving images
- Needs to be fast

## Why do we need this?

Email development has come a long way in terms of **what** is possible but **how** email is coded still lacks far behind traditional web development. Email still uses `<table>` for layout although `<div>` is becoming more popular each day.

Security concerns prevent us from using scripts such as JavaScript in email, not to mention it would immediately be spammed. People and companies are still using software like Outlook 2010 so cross-platform support for certain elements and layouts is about as messy as those \$1 DVD bins.

In general, Email is largely static, boring, and struggles to capture your target market's attention. So what can we do about this?

## Introducing dynamically generated imagery

One thing that works on 99% of email clients is images. So we focus our attention on improving that. Using dynamic images allows us to personalize the email to the reader with great custom fonts, designs and even custom animated GIF's to grab the reader's attention.

![Personalized email header](/images/canvasdemo1.jpg)

The above example is personalizing the header of the email with the recipients first name in a custom font on a background image.

## Let's get building

In summary we are going to build a simple Express server with NodeJS. This uses the node-canvas module to draw exactly what we want before exporting the canvas as a PNG.

### Initialise a project and install the dependencies

```bash
$ npm init
$ npm install express --save
$ npm install canvas --save
```

### Create server.js and require the dependencies needed

Don't forget to register your font files.

```javascript
const express = require("express");
const { registerFont, createCanvas, loadImage } = require("canvas");
const app = express();
const port = 3000;

// We need to register our font file to be used in canvas
registerFont("./fonts/Sign-Painter-Regular.ttf", { family: "signpainter" });

app.get("/", (req, res) => {
	res.send("Hello World!");
});

app.listen(port, () =>
	console.log(`Example app listening at http://localhost:${port}`)
);
```

If all is working you should be able to start your application with `node server` and visit your `hello world` at `http://localhost:3000`

### Create a custom GET route for the image

This should pull in the query parameters to be used in the canvas. In our case, we just want the name so all we have to do is:

```javascript
app.get("/header", (req, res) => {
	// Grab first name from query
	let firstname = decodeURI(req.query.name);

	// Custom canvas added here
	// ...
	// ...
});
```

### Add your canvas logic inside the route

From our design we know that the only personalization is going to be the first name. So the rest of it can be a "background-image" so to speak.

```javascript
app.get('/header', (req, res) => {

    // Grab first name from query
    let firstname = decodeURI(req.query.name) + "!";

    // Define the canvas
    const width = 600 // width of the image
    const height = 474 // height of the image
    const canvas = createCanvas(width, height)
    const context = canvas.getContext('2d')

    // Define the font style
    context.textAlign = 'center'
    context.textBaseline = 'top'
    context.fillStyle = '#FFFFFF'
    context.font = "80px 'signpainter' bold";

    // Load and draw the background image first
    loadImage('./images/background.jpg').then(image => {

        // Draw the background
        context.drawImage(image, 0, 0, 600, 474)

        // Draw the text
        context.fillText(firstname, 300, 150)

        // Convert the Canvas to a buffer
        const buffer = canvas.toBuffer('image/png')

        // Set and send the response as a PNG
        res.set({ 'Content-Type': 'image/png' });
        res.send(buffer)
    })
})
})
```

After drawing the background image and text, we are then converting the canvas into a buffer and sending the response back to the client as a PNG image. This allows the client to load the dynamic image on their side.

## Time to run this.

Start your app with `node server` and visit the new route you created at

```html
http://localhost:3000/header?name=@Sudo_Overflow
```

### And there you have it

![Dynamically generated image](/images/canvasdemo2.png)

You can now merge the first name into your email's `<img>` tag and have it automatically generated for you.

```html
<img src="http://localhost:3000/header?name=%%FirstName%%" />
```

---

A special thank you to [@flaviocopes](https://twitter.com/flaviocopes) for the idea of using Canvas. You can check out his article [here](https://flaviocopes.com/canvas-node-generate-image/).

The full project can be found on my [Github](https://github.com/CyrisXD/dynamic-image-generator)

If you know of ways to improve this or have feedback, let me know in the comments or Twitter at [@sudo_overflow](https://twitter.com/sudo_overflow)
