# jQuery.whenAll()

**`$.whenAll()`** is a small utility function that, like `$.when()` that it decorates,
aggregates multiple promises into a single promise, but unlike the later, it **always waits** for all promises
to have a final state, either resolved or rejected, before finalizing the returned promise.

The function also supports the unique jQuery Deferred `progress` notifications and implements its own notifying rules
for the returned promise (see the respective comment in [Usage](#usage)).

## Usage

```js
$.whenAll(promise1, promise2) // promise3, ...
	.done(function() {
		// Called when all promises are resolved
	})
	.fail(function() {
		/*
		 Called when all promises have a final state (resolved/rejected),
		 and at least one of them is rejected.
		 */
	})
	.always(function() {
		// Called when all promises have a final state (resolved/rejected)
	})
	.progress(function() {
		/*
		 Initially called when at least one promise notified a "progress"
		 by deferred.notify(), and all other promises are either
		 resolved/rejected/progressed.
		 After that, this callback will continue to be invoked for each
		 individual pending promise "progress" notification, until all
		 of them are finalized.
		 */
	});
```