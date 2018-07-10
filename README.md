# SharedLocationManager

A single location manager that allows developers to subscribe to location events

Importing

1. Clone repo and build
2. Copy framework into your target project.
3. Copy EventBroker framework into target project (if needed).
4. In the Copy Files build phase add EventBroker.framework and SharedLocationManager.framework to the Frameworks Destination


Usage

SharedLocationManager provides a single sharedLocationManager for use through out the app. Location related events are handled by a custom LocationManagerDelegate (which has adopted the entire CLLocationManagerDelegate protocol).

LocationManagerDelegate is also a publish/subscribe EventBroker. Components can subscribe/unsubscribe to/from location events via methods in sharedLocationService.  As specific delegate methods are called, they will publish the corresponding locationevent (e.g. locationManager(_: didUpdateLocations locations:))

LocationManager is a subclass of CLLocationManager and inherits all of its methods.  Developers will use this methods to initiate location-related services and actions (e.g. startUpdatingLocations())

Any hashable component can subscribe to location events via the subscribe(to: subscriber: handler:) method of sharedLocationManager. The handler is a closure that specifies the code to execute by the Subscriber when the location event is published. Subscribers must adaopt the Hashable protocol

Subscribers can unsubscribe to an event by calling unsubscribe(to event:, subscriber:) on sharedLocationManager
