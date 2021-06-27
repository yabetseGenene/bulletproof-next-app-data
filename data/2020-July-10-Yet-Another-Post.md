# Logger Bot

# General

In order for logger bot to work, bot privacy mode has to be changed to `Disabled` in **BotFather**.

[General Log Model](https://www.notion.so/aead2b6b5cde49a7996b0ba5923ebbd5)

### Downloading a File

We can get the file path using the [getFile](https://core.telegram.org/bots/api#getfile) method. `getFile` accepts **file_id** as an argument and returns an object that defines a *transient file path* along with other file info. 

The file path is valid only for an hour

```jsx
{
  file_id: 'AwACAgQAAxkBAAMmX3ymzPVKhibiUmJY36ymn9-g1SQAAlYHAAKIC-BT2FKOibBfgPAbBA',
  file_unique_id: 'AgADVgcAAogL4FM',
  file_size: 841,
  file_path: 'voice/file_4.oga'
}
```

For a reference, take a look at the below snippet to get the file [url]() for a voice message

```jsx
const fileID = ctx.message.voice.file_id;
ctx.telegram
  .getFile(fileID)
  .then((file) => {
    if (file != null) {
      let filePath = file.file_path;
      let fileUrl = `https://api.telegram.org/file/bot${process.env.TELEGRAM_BOT_TOKEN}/${filePath}`;
      console.log(fileUrl);
    }
  })
  .catch((error) => console.log(error));
```

### What is MIME?

> MIME stands for Multipurpose Internet Mail Extensions. It's a way of identifying files on the Internet according to their nature and format.

[Common MIME types](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/MIME_types/Common_types)

# Models

## Text

last_name or first name might not exist if the user haven't set it

```jsx
{
message_id: 8,
  from: {
    id: 205741803,
    is_bot: false,
    first_name: 'Yabetse',
    username: 'Yabetse',
    language_code: 'en'
  },
  chat: {
    id: -334412777,
    title: 'infra.net.group',
    type: 'group',
    all_members_are_administrators: true
  },
  date: 1601989947,
  text: 'this is dumb'
}
```

[Text Log Model](https://www.notion.so/35e92ec748ed49ad98c68c2288d9e9cf)

## File

[File Log Model](https://www.notion.so/bff494e7924048afb042effd75cf47c7)

## Voice [Extends File]

```jsx
{
  message_id: 32,
  from: {
    id: 205741803,
    is_bot: false,
    first_name: 'Yabetse',
    username: 'Yabetse',
    language_code: 'en'
  },
  chat: {
    id: -334412777,
    title: 'infra.net.group',
    type: 'group',
    all_members_are_administrators: true
  },
  date: 1602000462,
  voice: {
    duration: 1,
    mime_type: 'audio/ogg',
    file_id: 'AwACAgQAAxkBAAMgX3yWTlUWLtHzsAM_DWMoQ1ijoNkAAk0HAAKIC-BThp0ZBfgqlusbBA',
    file_unique_id: 'AgADTQcAAogL4FM',
    file_size: 3642
  }
}
```

[Voice Log Model](https://www.notion.so/e7b5d1c21cde4f1ba02be6aa49044f59)

## Document [Extends File]

```jsx
{
	// ...
  document: {
    file_name: 'girdosh.json',
    mime_type: 'application/json',
    file_id: 'BQACAgQAAxkBAAMoX3yplNgTnPrzdOuv12qNwcY16dsAAlgHAAKIC-BTVZ0GRjS9YEMbBA',
    file_unique_id: 'AgADWAcAAogL4FM',
    file_size: 25766
  }
}
```

[Document Log Model](https://www.notion.so/8555b776483148b6ad86392b3b423ad6)

## Photo [Extends File]

```jsx
{
	//...
  photo: [
    {
      file_id: 'AgACAgQAAxkBAAMpX3y2xaDOHVN_RlCPj_uQ0btWbRIAAqCyMRuIC-BTJPqi7_6SFDoKhCAnXQADAQADAgADbQADWP0AAhsE',
      file_unique_id: 'AQADCoQgJ10AA1j9AAI',
      file_size: 17906,
      width: 300,
      height: 300
    }
  ]
}
```

If a photo has a caption, the message object includes a `caption` property.

```jsx
photo: [
    {
      file_id: 'AgACAgQAAxkBAAMqX3y3CMA21f_tKyga9uvB-K3zC3oAAqCyMRuIC-BTJPqi7_6SFDoKhCAnXQADAQADAgADbQADWP0AAhsE',
      file_unique_id: 'AQADCoQgJ10AA1j9AAI',
      file_size: 17906,
      width: 300,
      height: 300
    }
  ],
caption: 'what a frame'
```

If a photo is sent as a file, the message type is going to be **document** with a mime type `'image/png'`. Furthermore, a thumbnail sent with the message. To represent the thumbnail, the document object defines a **thumb** object.

```jsx
document: {
  file_name: 'frame.png',
  mime_type: 'image/png',
  thumb: {
    file_id: 'AAMCBAADGQEAAytffLjL-Xpq4VXUAV1IkcGwM5b5OQACXgcAAogL4FMrwpjsNesOcLILtiddAAMBAAdtAANGTgACGwQ',
    file_unique_id: 'AQADsgu2J10AA0ZOAAI',
    file_size: 22968,
    width: 300,
    height: 300
  },
  file_id: 'BQACAgQAAxkBAAMrX3y4y_l6auFV1AFdSJHBsDOW-TkAAl4HAAKIC-BTK8KY7DXrDnAbBA',
  file_unique_id: 'AgADXgcAAogL4FM',
  file_size: 4785
}
```

[Photo Log Model](https://www.notion.so/fcb86f88d24b46039871684a64f92fcb)

## Sticker [Extends File]

```jsx
{
	// ...
	sticker: {
	  width: 512,
	  height: 512,
	  emoji: '👍',
	  set_name: 'BlueBird',
	  is_animated: true,
	  thumb: {
	    file_id: 'AAMCAgADGQEAAyxffL34sYgrCowtsICY3JRzxT1GbwAC9goAAi8P8AatkrBMm8R2V5qISA8ABAEAB20AA2hDAAIbBA',
	    file_unique_id: 'AQADmohIDwAEaEMAAg',
	    file_size: 5390,
	    width: 128,
	    height: 128
	  },
	  file_id: 'CAACAgIAAxkBAAMsX3y9-LGIKwqMLbCAmNyUc8U9Rm8AAvYKAAIvD_AGrZKwTJvEdlcbBA',
	  file_unique_id: 'AgAD9goAAi8P8AY',
	  file_size: 9212
	}
}
```

[Sticker Log Model](https://www.notion.so/d6068d3f522b4837b907c33475df5246)

## Video & GIF [Extends File]

```jsx
{

	//..
	video: {
    duration: 21,
    width: 772,
    height: 1588,
    mime_type: 'video/mp4',
    thumb: {
      file_id: 'AAMCBAADGQEAAzFffMfS8BhBUaejDIJzJNm9wNyVtwACZAcAAogL4FN1vjrlUJSP6OHIwyddAAMBAAdtAAO3OgACGwQ',
      file_unique_id: 'AQAD4cjDJ10AA7c6AAI',
      file_size: 1052,
      width: 156,
      height: 320
    },
    file_id: 'BAACAgQAAxkBAAMxX3zH0vAYQVGnowyCcyTZvcDclbcAAmQHAAKIC-BTdb465VCUj-gbBA',
    file_unique_id: 'AgADZAcAAogL4FM',
    file_size: 2356962
  }
}
```

A message type is set as a **video** if it's uploaded as a file, otherwise it's a document with an accompanying animation object. 

```jsx
{
	//...
	animation: {
    file_name: 'girdosh.mp4',
    mime_type: 'video/mp4',
    duration: 10,
    width: 772,
    height: 1588,
    thumb: {
      file_id: 'AAMCBAADGQEAAzJffM-BEHLxcwNENgJMtgtk1bRoNgACaQcAAogL4FPAvdQAAbsnYYtshZcnXQADAQAHbQADyS4AAhsE',
      file_unique_id: 'AQADbIWXJ10AA8kuAAI',
      file_size: 1522,
      width: 156,
      height: 320
    },
    file_id: 'CgACAgQAAxkBAAMyX3zPgRBy8XMDRDYCTLYLZNW0aDYAAmkHAAKIC-BTwL3UAAG7J2GLGwQ',
    file_unique_id: 'AgADaQcAAogL4FM',
    file_size: 2545353
  },
  document: {
    file_name: 'girdosh.mp4',
    mime_type: 'video/mp4',
    thumb: {
      file_id: 'AAMCBAADGQEAAzJffM-BEHLxcwNENgJMtgtk1bRoNgACaQcAAogL4FPAvdQAAbsnYYtshZcnXQADAQAHbQADyS4AAhsE',
      file_unique_id: 'AQADbIWXJ10AA8kuAAI',
      file_size: 1522,
      width: 156,
      height: 320
    },
    file_id: 'CgACAgQAAxkBAAMyX3zPgRBy8XMDRDYCTLYLZNW0aDYAAmkHAAKIC-BTwL3UAAG7J2GLGwQ',
    file_unique_id: 'AgADaQcAAogL4FM',
    file_size: 2545353
  }
}
```

The Above format applies to gif since gifs are .mp4 files

[Video Log Model](https://www.notion.so/006a012bb55e4fd5b54adb4f143559fa)

## Audio [Extends File]

```jsx
{
	// ..
	audio: {
	    duration: 350,
	    mime_type: 'audio/mpeg3',
	    title: 'Superman',
	    performer: 'Eminem;Dina Rae',
	    file_id: 'CQACAgQAAxkBAAM2X3zavQvQzamNrODsvjJTcpmUhOgAAm4HAAKIC-BTT-ztHAvPKWEbBA',
	    file_unique_id: 'AgADbgcAAogL4FM',
	    file_size: 14140136
	 }
}
```

[Audio Log Model](https://www.notion.so/9168ed3a17c34ede979ec83db58d5293)

## Contact

```jsx
{
	//...
	contact: {
	  phone_number: '251936695958',
	  first_name: 'Jhon',
	  user_id: 325354008
	}
}
```

[Contact Log Model](https://www.notion.so/49fc76b0f6ba4731864cf5665df94b7d)

## ChannelPost

In order for the bot to treat channel posts as messages, set channelMode option to true when creating the bot instance.

```jsx
const bot = new Telegraf(process.env.TELEGRAM_BOT_TOKEN, { channelMode: true });
```

channel post instance

```jsx
{
  message_id: 24,
  chat: { id: -1001293643361, title: 'infra.net', type: 'channel' },
  date: 1601997518,
  text: 'it is nice'
}
```

User info is not specified because only an admin can post messages

If a post is edited, `edit_date` property is added to channel_post object.

```jsx
{
  message_id: 24,
  chat: { id: -1001293643361, title: 'infra.net', type: 'channel' },
  date: 1601997518,
  edit_date: 1601998337,
  text: 'it is not nice'
}
```
