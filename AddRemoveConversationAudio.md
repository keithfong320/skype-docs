
# Add or remove audio in a conversation

 **Last modified:** April 23, 2015

 _**Applies to:** Skype for Business 2015_

 **In this article**
[Adding audio to a conversation](#sectionSection0)
[Removing audio from a conversation](#sectionSection1)
[Subscribing to changes from the audioService in a conversation](#sectionSection2)
[Accepting video and sending video automatically](#sectionSection3)
[Muting a conversation](#sectionSection4)
[Putting a conversation on Hold](#sectionSection5)


With an existing conversation instance, audio can be added or removed. 

## Adding audio to a conversation
<a name="sectionSection0"> </a>


1. 


  ```js
  conversation.audioService.start().then(function () {
	// Successfully added audio to the conversation
});

  ```


## Removing audio from a conversation
<a name="sectionSection1"> </a>


1. 


  ```js
  Conversation.audioService.stop().then(function () {
	// Successfully removed audio from the conversation
});

  ```


## Subscribing to changes from the audioService in a conversation
<a name="sectionSection2"> </a>

An event is fired when the client has successfully added audio to the conversation, or another participant has invited the client to add audio. 


1. Subscribe to the event.
    

  ```js
  conversation.selfParticipant.audio.state.changed(function (val) {
…
});

  ```

2. If the val argument in the previous snippet indicates the event is an invitation to add audio, the client may reject or accept the invitation.
    

  ```js
  if (val == 'Notified') {
    if (confirm('Accept incoming audio request?')) {
        console.log('accepting the incoming audio request');
        conversation.audioService.accept();
        console.log('Accepting incoming audio request');
    } else {
        console.log('declining the incoming audio request');
        conversation.audioService.reject();
    }
}
  ```


## Accepting video and sending video automatically
<a name="sectionSection3"> </a>

Calling videoService.accept() in response to an audio invitation will do nothing. Calling videoService.accept() in response to a video invitation will accept the audio and video and start own video as well.


1. Subscribe to the audio state changed event:
    

  ```js
  conversation.selfParticipant.audio.state.changed(function (val) {
…
});

  ```

2. If the val argument in the previous snippet indicates the event is an invitation to add audio, the client may accept the invitation while also sending their own video in Skype with the following:

    
  ```js
  if (val == 'Notified') {
conversation.videoService.accept();
}

  ```


## Muting a conversation
<a name="sectionSection4"> </a>


1. The client may temporarily mute their own audio in the conversation.
    

  ```js
  // Toggle muting the client's audio
conversation.selfParticipant.audio.isMuted.set(!audio.isMuted());

  ```


## Putting a conversation on Hold
<a name="sectionSection5"> </a>


1. The client may also place itself on hold, temporarily pausing all incoming and outgoing audio.
    

  ```js
  // Toggle placing the conversation on hold
var isOnHold = conversation.selfParticipant.audio.isOnHold();
conversation.selfParticipant.audio.isOnHold.set(!isOnHold);

  ```
