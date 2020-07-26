ervice States in Icinga2
* 0 UP   OK       :            WORKING WELL
* 1 UP   WARNING  :      MIGHT LIGHT MIGHT BE OUT, BUT I WORK!
* 2 DOWN CRITICAL :      I AM GOING DOWN! 
* 3 DOWN UNKNOW   :      COULD NOT DETERMINE STATUS

### Host and Service Checks 
The state is determined by running checks in regular intervals

```js
object Host "router" {
  check_command = "hostalive"
  address = "10.0.0.1"
}
```
`hostalive`
* Built in
* sends ICMP echo requests to the IP in address
* hostalive is same as ping except default thresholds
* for faster ICMP checks look into icmp checkCommand

### Host check alternatives

If host is not reachable with icmp, one can use dummy state to set a default state.

```js
object Host "dummy-host" {
  check_command = "dummy"
  vars.dummy_state = 0 // refer to table above for what it means uWu
  vars.dummy_text = "All is well!"
}
```
### Templates 
* used for applying a set of identical attributes to more than one object

```js
template Service "generic-service" {
  max_check_attempts = 3
  check_interval = 5m
  retry_interval = 1m
  enable_perfdata = true
}

apply Service "ping4" {
  import "generic-service"
  check_command = "ping4"
  assign where host.address
}

apply Service "ping6" {
  import "generic-service"
  check_command = "ping6"
  assign where host.address6
}
```

*Note* : Templates and Objects share same namespace, you can't define a template that has the same name like an object.


