- trigger types
  <table aria-label="Table 1" class="table table-sm">
  <thead>
  <tr>
  <th>Type</th>
  <th>Description</th>
  </tr>
  </thead>
  <tbody>
  <tr>
  <td>Phrases</td>
  <td>Topic is triggered when one or more of the trigger phrases match with the incoming message from a user</td>
  </tr>
  <tr>
  <td>Activity Received</td>
  <td>Topic is triggered when an Activity of any type is received</td>
  </tr>
  <tr>
  <td>Message Received</td>
  <td>Topic is triggered when an Activity of type <em><strong>message</strong></em> is received. This is the most common type of Activity and they are received when a user types or says something to a bot</td>
  </tr>
  <tr>
  <td>Event Received</td>
  <td>Topic is triggered when an Activity of type <em><strong>event</strong></em> is received</td>
  </tr>
  <tr>
  <td>Conversation update received</td>
  <td>Topic is triggered when an Activity of type <em><strong>conversationupdate</strong></em> is received. e.g. Microsoft Teams sends an activity of this type when a user joins a conversation</td>
  </tr>
  <tr>
  <td>Invoke received</td>
  <td>Topic is triggered when an Activity of type <em><strong>invoke</strong></em> is received. Most commonly received from the Microsoft Teams channel, when the user interacts with a Teams app, such as a Message or Search extension</td>
  </tr>
  <tr>
  <td>Inactivity</td>
  <td>Topic is triggered when a user has not interacted with the bot for a period of time. The time period can be configured.</td>
  </tr>
  </tbody>
  </table>