- [Functional Event Sourcing Decider](https://thinkbeforecoding.com/post/2021/12/17/functional-event-sourcing-decider)
	- ![](https://thinkbeforecoding.com/public/functional-event-sourcing-decider/diagram-8.svg)
	- ``` f#
	  module WithSnapshotsInContainers =
	      let start (decider: Decider<'c,'e,'s>) =
	          let container = getContainerFromDecideHash(decider)
	          // load state using snapshot if any
	          let loadState stream =
	              // load snapshot.. it will not be found if container has
	              // changed since last run
	              let snapVersion, snapState =
	                  SnapshotsWithContainer.tryLoadSnapshot(stream, container)
	                      // fallback to version 0 and initialState if not found
	                  |> Option.defaultValue (0, decider.initialState)
	  
	              // load version and events after snapshot
	              let version, events =
	                  EventStoreWithVersion.loadEvents(stream, snapVersion)
	              // fold events after snapshot
	              let state = List.fold decider.evolve snapState events
	              version, state
	  
	          fun stream (command: 'c) ->
	              let rec handle (version, state) =
	                  // get events from the decision
	                  let events = decider.decide command state
	                  // append events to stream
	                  match EventStoreWithVersion.tryAppendEvents(stream, version, events) with
	                  | Ok newVersion ->
	                      if isTimeToSnapshot version then
	                          // it is time to save snapshot
	                          // compute state
	                          let newState = List.fold decider.evolve state events
	                          // save it
	                          SnapshotsWithContainer.saveSnapshot(stream, container, newVersion, newState)
	                      events
	                  | Error(actualVersion, catchupEvents) ->
	                      // there was a concurrent write
	                      // catch-up missing events and retry
	                      let actualState = List.fold decider.evolve state catchupEvents
	                      handle (actualVersion, actualState)
	  
	  
	              // load all past events to compute current state
	              // using snapshot if any
	              let version, state = loadState stream
	              handle (version, state)
	  
	  ```