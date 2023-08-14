# React-based Chatroom Component for Rasa Stack



<a href="https://npm-scalableminds.s3.eu-central-1.amazonaws.com/@scalableminds/chatroom@master/demo.html"><img src="https://npm-scalableminds.s3.amazonaws.com/%40scalableminds/chatroom/demo.gif" alt="Demo" width="409" height="645" /></a>

**Note: This project is forked from an archived project. Is not maintained anymore. If you like to become a community maintainer go to the original [repo](https://github.com/scalableminds/chatroom) and get in touch with @hotzenklotz.**

The project works up to Rasa 3 (current version). Here, it has got some minor updates.

## Features

* React-based component
* Simple setup. Works with Rasa's [REST channel](https://rasa.com/docs/rasa/user-guide/connectors/your-own-website/#rest-channels)
* Supports Text with Markdown formatting, Images, and Buttons
* Generates a unique session id and keeps it in `sessionStorage`
* Queues consecutive bot messages for better readability
* Speech input (only in Chrome for now)
* Text to Speech (depending on your browser, works in Chrome and Firefox)
* Demo mode included (ideal for scripted screencasts)
* Hosted on Github for easy use
* Customizable without rebuilding. Comes with three example themes *theme1*, *theme2*, and *theme3*
* Customizable welcomeMessage and welcomeButtons show when openend

## Usage
1. Embed the `chatroom.js` in the HTML of your website and configure it to connect to your Rasa bot. Either use the hosted version or build it yourself. (see below)

```html
<head>
  <link rel="stylesheet" href="https://cdn.statically.io/gh/weberi/chatroom/master/dist/Chatroom.css" />
  <link rel="stylesheet" type="text/css" href="https://cdn.statically.io/gh/weberi/chatroom/master/index.css">
  <!-- <link rel="stylesheet" type="text/css" href="https://cdn.statically.io/gh/weberi/chatroom/master/themes/theme3.css" /> --> 
</head>
<body>
  <div class="chat-container"></div>
  <script src="https://cdn.statically.io/gh/weberi/chatroom/master/dist/Chatroom.js"></script>

  <script type="text/javascript">
    var chatroom = new window.Chatroom({
      host: "http://localhost:5005",
      title: "Chat with a Bot",
      container: document.querySelector(".chat-container"),
      welcomeMessage: "Hi, I am a Bot. How may I help you?",
      welcomeButtons: [
          { title: "Hello", payload: "\greet" },
          { title: "GoodBye", payload: "\goodbye" }
        ],
      speechRecognition: "en-US",
      voiceLang: "en-US"
    });
    chatroom.openChat();
  </script>
</body>
```


2. In your Rasa bot setup, make sure to include the Rasa [REST channel](https://rasa.com/docs/rasa/user-guide/connectors/your-own-website/#rest-channels) in your `credentials.yml` file:
```
rest:
  # pass
```

Restart your Rasa server. Depending on your setup you might need to add CORS headers, e.g. `--cors "*"`.

```
rasa run --credentials ./credentials.yml  --enable-api --auth-token XYZ123 --model ./models --endpoints ./endpoints.yml --cors "*"
```

Note, the version of the Chatroom's Javascript file is encoded in the URL. `chatroom@master` is always the latest version from the GitHub master branch. Use e.g. `chatroom@0.10.0` to load a specific release. [All Releases can be found here.](https://github.com/scalableminds/chatroom/releases)


| Chatroom Version  | Compatible Rasa Core Version |
|-------------------|------------------------------|
| 0.13.x            | 1.0 - 3.x                    |
| 0.10.x            | 1.0 - 2.x                    |
| 0.9.x (Deprecated)| 0.11.4+, 0.13.7              |
| 0.8.x (Deprecated)| 0.11.4+                      |
| 0.7.8 (Deprecated)| 0.10.4+                      |

Note, versions prior to `0.10.x` used a custom Python channel to connect the chatroom frontend with a Rasa bot backend. Upgrading, from version `0.9.x` or below will require you to modify the `credentials.yml` and include the Rasa REST channel. (see installation instructions above)


## Development

### Install dependencies

```
yarn install
```

### Continuously build the Chatroom component

```
yarn watch
yarn serve
```

Open `http://localhost:8080/demo.html` in your browser.

## Build

```
yarn build
```

Distributable files will be created in folder `dist`.

## License

AGPL v3

Made by [scalable minds](https://scalableminds.com), some small adaptions by weberi
