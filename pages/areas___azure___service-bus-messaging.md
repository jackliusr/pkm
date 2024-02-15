- Compare Storage queues and Service Bus queues
	- Foundational capabilities
		- <table aria-label="Table 1" class="table table-sm">
		  <thead>
		  <tr>
		  <th>Comparison Criteria</th>
		  <th>Storage queues</th>
		  <th>Service Bus queues</th>
		  </tr>
		  </thead>
		  <tbody>
		  <tr>
		  <td>Ordering guarantee</td>
		  <td>No <br><br>For more information, see the first note in the <a href="#additional-information" data-linktype="self-bookmark">Additional Information</a> section.<br></td>
		  <td>Yes - First-In-First-Out (FIFO)<br><br>(by using <a href="message-sessions" data-linktype="relative-path">message sessions</a>)</td>
		  </tr>
		  <tr>
		  <td>Delivery guarantee</td>
		  <td>At-Least-Once</td>
		  <td>At-Least-Once (using PeekLock receive mode. It's the default) <br><br>At-Most-Once (using ReceiveAndDelete receive mode) <br> <br> Learn more about various <a href="service-bus-queues-topics-subscriptions#receive-modes" data-linktype="relative-path">Receive modes</a></td>
		  </tr>
		  <tr>
		  <td>Atomic operation support</td>
		  <td>No</td>
		  <td>Yes<br><br></td>
		  </tr>
		  <tr>
		  <td>Receive behavior</td>
		  <td>Non-blocking<br><br>(completes immediately if no new message is found)</td>
		  <td>Blocking with or without a timeout<br><br>(offers long polling, or the <a href="https://go.microsoft.com/fwlink/?LinkId=613759" data-linktype="external">"Comet technique"</a>)<br><br>Non-blocking<br><br>(using .NET managed API only)</td>
		  </tr>
		  <tr>
		  <td>Push-style API</td>
		  <td>No</td>
		  <td>Yes<br><br>Our .NET, Java, JavaScript, and Go SDKs provide push-style API.</td>
		  </tr>
		  <tr>
		  <td>Receive mode</td>
		  <td>Peek &amp; Lease</td>
		  <td>Peek &amp; Lock<br><br>Receive &amp; Delete</td>
		  </tr>
		  <tr>
		  <td>Exclusive access mode</td>
		  <td>Lease-based</td>
		  <td>Lock-based</td>
		  </tr>
		  <tr>
		  <td>Lease/Lock duration</td>
		  <td>30 seconds (default)<br><br>7 days (maximum) (You can renew or release a message lease using the <a href="/en-us/dotnet/api/microsoft.azure.storage.queue.cloudqueue.updatemessage" data-linktype="absolute-path">UpdateMessage</a> API.)</td>
		  <td>30 seconds (default)<br><br>You can renew the message lock for the same lock duration each time manually or use the automatic lock renewal feature where the client manages lock renewal for you.</td>
		  </tr>
		  <tr>
		  <td>Lease/Lock precision</td>
		  <td>Message level<br><br>Each message can have a different timeout value, which you can then update as needed while processing the message, by using the <a href="/en-us/dotnet/api/microsoft.azure.storage.queue.cloudqueue.updatemessage" data-linktype="absolute-path">UpdateMessage</a> API.</td>
		  <td>Queue level<br><br>(each queue has a lock precision applied to all of its messages, but the lock can be renewed as described in the previous row)</td>
		  </tr>
		  <tr>
		  <td>Batched receive</td>
		  <td>Yes<br><br>(explicitly specifying message count when retrieving messages, up to a maximum of 32 messages)</td>
		  <td>Yes<br><br>(implicitly enabling a pre-fetch property or explicitly by using transactions)</td>
		  </tr>
		  <tr>
		  <td>Batched send</td>
		  <td>No</td>
		  <td>Yes<br><br>(by using transactions or client-side batching)</td>
		  </tr>
		  </tbody>
		  </table>
	- Advanced capabilities
		- <table aria-label="Table 2" class="table table-sm">
		  <thead>
		  <tr>
		  <th>Comparison Criteria</th>
		  <th>Storage queues</th>
		  <th>Service Bus queues</th>
		  </tr>
		  </thead>
		  <tbody>
		  <tr>
		  <td>Scheduled delivery</td>
		  <td>Yes</td>
		  <td>Yes</td>
		  </tr>
		  <tr>
		  <td>Automatic dead lettering</td>
		  <td>No</td>
		  <td>Yes</td>
		  </tr>
		  <tr>
		  <td>Increasing queue time-to-live value</td>
		  <td>Yes<br><br>(via in-place update of visibility timeout)</td>
		  <td>Yes<br><br>(provided via a dedicated API function)</td>
		  </tr>
		  <tr>
		  <td>Poison message support</td>
		  <td>Yes</td>
		  <td>Yes</td>
		  </tr>
		  <tr>
		  <td>In-place update</td>
		  <td>Yes</td>
		  <td>Yes</td>
		  </tr>
		  <tr>
		  <td>Server-side transaction log</td>
		  <td>Yes</td>
		  <td>No</td>
		  </tr>
		  <tr>
		  <td>Storage metrics</td>
		  <td>Yes<br><br>Minute Metrics provides real-time metrics for availability, TPS, API call counts, error counts, and more. They're all in real time, aggregated per minute and reported within a few minutes from what just happened in production. For more information, see <a href="/en-us/rest/api/storageservices/fileservices/About-Storage-Analytics-Metrics" data-linktype="absolute-path">About Storage Analytics Metrics</a>.</td>
		  <td>Yes<br><br>For information about metrics supported by Azure Service Bus, see <a href="monitor-service-bus-reference#message-metrics" data-linktype="relative-path">Message metrics</a>.</td>
		  </tr>
		  <tr>
		  <td>State management</td>
		  <td>No</td>
		  <td>Yes (Active, Disabled, SendDisabled, ReceiveDisabled. For details on these states, see <a href="entity-suspend#queue-status" data-linktype="relative-path">Queue status</a>)</td>
		  </tr>
		  <tr>
		  <td>Message autoforwarding</td>
		  <td>No</td>
		  <td>Yes</td>
		  </tr>
		  <tr>
		  <td>Purge queue function</td>
		  <td>Yes</td>
		  <td>No</td>
		  </tr>
		  <tr>
		  <td>Message groups</td>
		  <td>No</td>
		  <td>Yes<br><br>(by using messaging sessions)</td>
		  </tr>
		  <tr>
		  <td>Application state per message group</td>
		  <td>No</td>
		  <td>Yes</td>
		  </tr>
		  <tr>
		  <td>Duplicate detection</td>
		  <td>No</td>
		  <td>Yes<br><br>(configurable on the sender side)</td>
		  </tr>
		  <tr>
		  <td>Browsing message groups</td>
		  <td>No</td>
		  <td>Yes</td>
		  </tr>
		  <tr>
		  <td>Fetching message sessions by ID</td>
		  <td>No</td>
		  <td>Yes</td>
		  </tr>
		  </tbody>
		  </table>