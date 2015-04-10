# Poller.tcl

Common pattern that kept coming up when talking to devices.

1. Send a "request for status" message to the device
2. Wait until the device has had sufficient time to process the request and respond to us
3. Read the response
4. If there was a response, postpone the "timeout" action
5. Go back to polling
6. If the timeout action ever fires, stop the polling cycle


**Example Usage:**
```
package require poller

proc send_request {} {
  puts "send the 'request status' message to the device."
}

proc read_response {} {
  puts "read the status response from the device, if we got back what we wanted, postpone the timeout."
}

proc handle_timeout {} {
  puts "we timed out, so do something else like switch to another port and start polling there."
}


poller create myPoller 1000 10000 send_request read_response handle_timeout
myPoller start
```
