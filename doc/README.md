# RaulM messaging API documentation

## Requests contract:

-This API receives http post requests at endpoint /message
-Request body should be a json with format 
 {
   "destination":"name",
   "body":"your message here" 
  }
-Number of requests is limited to 100 every 15 minutes

## API answer and errors format

If your message is sent correctly, the API will answer with an "OK" message in string
format and a 200 status. 

When the request fails, the API will answer with a string and one of this errors messages:

  -Server error. Check the request format. (Sytax error) || status 500

  You are probably not sending a valid json in the body of the post.

  -Bad format: destination and message should be strings || status 500

  Your body should include a json with the format shown in the previous point and
  the fields can not be left empty. Empty strings are not allowed either.

  -Server error when requesting the message service || status 500

  As you may know, this API works as a proxy of another service. If that messaging
  service fails, this error is sent.

  -Too many requests, please try again later. || status 429

  Requests are limited to a certain amount. Namely, 100 requests every 15 minutes.
  If you exceed over that limit, you will receive this message.
