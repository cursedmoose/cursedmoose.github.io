---
layout: post
author: cursedmoose
title:  Hellbot Update - Vision
date:   2023-11-09 12:15:00 -0800
category: update
---

Hellbot is watching me. 👀

Ever since OpenAI announced their [Vision capabilities](https://www.nytimes.com/2023/09/27/technology/new-chatgpt-can-see-hear.html) in September 2023, I've been eager to add this functionality to Hellbot.
More input is more hell is more better.

Having the ability to feed Hellbot with screen capture information, possibly even eventually in real time, allows the AI to feel more life-like and opens up huge new opportunities.

### The Vision API
OpenAI released the [Vision API Preview](https://platform.openai.com/docs/guides/vision) on November 6. Big thanks to [OpenAI.Net](https://github.com/RageAgainstThePixel/OpenAI-DotNet) for quickly implementing an API wrapper, so instead of this:


```
curl https://api.openai.com/v1/chat/completions \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -d '{
    "model": "gpt-4-vision-preview",
    "messages": [
      {
        "role": "user",
        "content": [
          {
            "type": "text",
            "text": "What’s in this image?"
          },
          {
            "type": "image_url",
            "image_url": {
              "url": "https://upload.wikimedia.org/wikipedia/commons/thumb/d/dd/Gfp-wisconsin-madison-the-nature-boardwalk.jpg/2560px-Gfp-wisconsin-madison-the-nature-boardwalk.jpg"
            }
          }
        ]
      }
    ],
    "max_tokens": 300
  }'
```

we just need to write this: 
```
var messages = new List<Message>
{
    new Message(Role.User, new List<Content>
    {
        new Content(ContentType.Text, "What's in this image?"),
        new Content(ContentType.ImageUrl, "https://upload.wikimedia.org/wikipedia/commons/thumb/d/dd/Gfp-wisconsin-madison-the-nature-boardwalk.jpg/2560px-Gfp-wisconsin-madison-the-nature-boardwalk.jpg")
    })
};
var chatRequest = new ChatRequest(messages, model: "gpt-4-vision-preview");
var result = await OpenAIClient.ChatEndpoint.GetCompletionAsync(chatRequest);
return result.FirstChoice;
```

Super easy thanks to a great library. The folks working on OpenAI.net are doing a great job.

### Sending My Screen
Originally I was looking into sending an image as a [base64 encoded string](https://platform.openai.com/docs/guides/vision/uploading-base-64-encoded-images) to avoid the problem of uploading images, but it quickly became apparent that wasn't going to work.

```
07/11/2023 13:40:38 [ChatGpt] [ERROR] Got error: GetCompletionAsync Failed! HTTP status code: TooManyRequests | Response body: {
    "error": {
        "message": "Rate limit reached for gpt-4-vision-preview in organization [redacted] on tokens per min. Limit: 40000 / min. Please try again in 1ms. Visit https://platform.openai.com/account/rate-limits to learn more.",
        "type": "tokens",
        "param": null,
        "code": "rate_limit_exceeded"
    }
}
```

Whoops. Even if it worked, at $0.03/1K tokens, 40,000 tokens is already costing me $1.20 per request. Way too much to be sending 100s a day.

Now this makes sense, Base64 encoded images are [~33% larger](https://en.wikipedia.org/wiki/Base64) than their image counterparts, and I wasn't doing any kind of image compression or resizing. But even if I was, compressing an image to a reasonable size (1KB maybe?) probably isn't going to be great.

|Original|1KB Compressed|
|--------|--------------|
|![hehehe](/assets/images/blog/hehehe2.png)|![ew](/assets/images/blog/hehehe2-1kb.png)|

Okay, so let's find a way to upload images!

#### Uploading Images
There are plenty of great image hosting sites out there right now. Imgur, Flickr, Tumblr, Dropbox, Google Drive, etc. The list goes on.
But rather than connecting to yet another service, what if I could accomplish this with an existing integration? I upload images on Discord all the time; they have to be stored somewhere and left accessible for at least enough time to react to them. It seemed like a perfect solution!

Enter my two favorite questions in programming:
1. Can I do it? (or, do the systems I have access to allow me to do it?)
2. How do I do it? (or, how do I leverage existing systems to do this?)

We can answer question 1 by searching the [Discord API](https://discord.com/developers/docs/intro) and sure enough, [we can](https://discord.com/developers/docs/reference#uploading-files).

Question 2 shouldn't be too hard to answer if we trust our [library (another stellar package)](https://discordnet.dev/), and with a little help from the IDE, we quickly find

 ```Task<IUserMessage> IMessageChannel.SendFileAsync(string filePath)```

 It even returns the message sent, complete with the URL to the attachment. Dang, what a good library.

#### Bringing it all together
 After a few helper functions, the final code we write looks something like:

 ```
var imageFile = Server.Instance.TakeScreenshot();
var fileUrl = await Server.Instance.Discord.UploadFile(imageFile);
Assistant.ReactToImage(fileUrl);
```

Super easy, super fun, super powerful.

### An Image is Worth 1000 words, 1000 words costs $0.03
The current implementation of Vision makes it a bit hard to eke out exactly what I'm looking for in a response.
The model typically tries to describe what the image contains (an important demo of understanding), but has a hard time creating a narrative around or reacting to the image. For example, a screencap of a dragon fight in Skyrim is more likely to elicit the description:

```"A tense moment in Skyrim: Dragon mid-flight, health low. Will the player land the next blow or retreat strategically? Adventure awaits in every frame."```

as opposed to a reaction:

```"Trying to fight a bloodthirsty dragon at low health? Looks like you're about to become dinner."```

Hopefully with a few more iterations, OpenAI will get there.

#### Anyways thanks for reading, I'm gonna go take vision-empowered Hellbot for a spin. 
### [Catch me live](/stream.html)!