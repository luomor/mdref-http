# http\Client http\Client::enqueue(http\Client\Request $request[, callable $cb])

Add another http\Client\Request to the request queue.
If the optional callback $cb returns true, the request will be automatically dequeued.

> ***Note:***  
> The http\Client\Response object resulting from the request is always stored 
> internally to be retreived at a later time, __even__ when $cb is used.
> 
> If you are about to send a lot of requests and do __not__ need the response
> after executing the callback, you can use http\Client::getResponse() within
> the callback to keep the memory usage level as low as possible.

See http\Client::dequeue() and http\Client::send().


## Params:

* http\Client\Request $request  
  The request to enqueue.
* Optional callable $cb  
  A callback to automatically call when the request has finished.

## Returns:

* http\Client, self.

## Throws:

* http\Exception\InvalidArgumentException
* http\Exception\BadMethodCallException
* http\Exception\RuntimeException

## Example:

    (new http\Client)->enqueue(new http\Client\Request("GET", "http://php.net"), 
        function(http\Client\Response $res) {
            printf("%s returned %d\n", $res->getTransferInfo("effective_url"), $res->getResponseCode());
            return true; // dequeue
    })->send();

Yields:

    http://php.net/ returned 200
