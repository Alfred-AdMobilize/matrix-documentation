# MatrixOS Config Widget examples

# Layout
![Screens](img/screens.png)
```
screens:
  - - cpu
    - memory
```

# Displays

## Value
![Value](img/value.png)
```
cpu:
  type: monitor
  key: cpu
  display: digit
  format: round
  label: cpu
```

## Bar Chart
![Bar Chart](img/bar.png)
```
barChart:
  type: monitor
  keys: cpu, memory
  display: bar
  label: Bar Chart
```

## Radar Chart
![Radar Chart](img/radar.png)
```
radarTest:
  type: monitor
  keys: cpu,memory
  display: radar
  label: radarTest
```

## Line Chart
![Line Chart](img/line.png)
```
cpuChart:
  type: monitor
  keys: cpu,memory
  display: line
  label: CPU Chart
```

## Lists
![List](img/secret.png)
```
info:
  type: device
  display: list-group
  label: Secret Information
```

# Interactive

## Buttons

### Single
![1 Button](img/1but.png)
```
buttonTest:
  label: Hacking Buttons
  control: button
  event: buttonInfo
  value: Get Secret Information
```
###### Handling Code
```
matrix.on('buttonInfo', function(){
  // ...
})
```
`event` in the config file, is the event name (`buttonInfo`) handled.


### Map Notation
Multiple events are supported in a widget through the use of the `map` property.

This has two valid expressions. Key / Value and Collection

#### Simple Form - Key, Value
```
buttons:
  control: button
  map:
    'label' : eventName
    'label2': event2Name
```


#### Simple Form - mapSort
Use `order` to display buttons in a particular order.

```
map:
  'label' : eventName
  'label2': event2Name
order:
  - 'label'
  - 'label2'
```

#### Normal Form - Multiple
```
buttons:
  control: button
  map:
   - value: seven
     event: event7
   - value: eight
     event: event8
   - value: nine
     event: event9
```

#### Normal Form Overview
```
map:
  - value: foo    # button label
    event: e     # event name emitted for app to listen for
    <!-- data: 1      # what data to send with this button -->
    <!-- color: 'red' # what color to tint this button -->
```

### Multiple
![Multi Button](img/nbut.png)
```
buttonsTest:
  label: Matrix Activation Buttons
  control: button
  map:
    'amps+': buttonUp
    'amps-': buttonDown
    begin : buttonStart
    end : buttonStop
    capture : buttonSample
    'refresh+' : buttonSlow
    'refresh-' : buttonFast
```
###### Handling Code
```
 matrix.on('buttonStop', function(){
   //...
})

 matrix.on('buttonStart', function(){
   //...
 })

 matrix.on('buttonSample', function () {
   //...
 })
```
## Drop Downs
![DropDown](img/drop.png)
```
dropDown:
  control: dropdown
  map:
    test1: doTest1
    test2: doTest2
  label: dropdown test
```
###### Handling Code
```
matrix.on('doTest1', function(){
 //...
})


matrix.on('doTest2', function(){
 //...
})
```

###### Handling Data
To group your apps

# Responsive Data Flow
```
matrix.on('buttonInfo', function(){
  matrix.type('device').send({
    'os_hostname': os.hostname(),
    'os_type': os.type(),
    'os_platform': os.platform(),
    'os_arch': os.arch()
  });
})
```
When `buttonInfo` is triggered, respond with information with a type `device`.

The list looks for
```
widgets:
  list:
    type: device
```
The `list` widget displays information of type `device`.
