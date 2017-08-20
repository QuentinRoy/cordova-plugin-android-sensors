# Cordova Android Sensors Plugin

This plugin gives access to android sensors.

## Install

```sh
cordova plugin add https://github.com/QuentinRoy/cordova-plugin-android-sensors.git
```


<a name="sensors"></a>

## sensors : <code>object</code>
**Kind**: global namespace  

* [sensors](#sensors) : <code>object</code>
    * [.addSensorListener(sensorType, samplingRate, listener, [callback])](#sensors.addSensorListener) ⇒ <code>undefined</code>
    * [.removeSensorListener(sensorType, samplingRate, listener, [callback])](#sensors.removeSensorListener) ⇒ <code>undefined</code>

<a name="sensors.addSensorListener"></a>

### sensors.addSensorListener(sensorType, samplingRate, listener, [callback]) ⇒ <code>undefined</code>
Add a sensor listener.

**Kind**: static method of [<code>sensors</code>](#sensors)  

| Param | Type | Description |
| --- | --- | --- |
| sensorType | <code>string</code> | the sensor type's constant name (as defined by [Android Sensor](https://developer.android.com/guide/topics/sensors/sensors_overview.html), but without the prefix `"TYPE_"`) |
| samplingRate | <code>string</code> | the sampling period's constant name (as accepted by [SensorManager#registerListener](https://developer.android.com/reference/android/hardware/SensorManager.html#registerListener(android.hardware.SensorEventListener,%20android.hardware.Sensor,%20int)) without the prefix `"SENSOR_DELAY_"`) |
| listener | [<code>sensorEventListener</code>](#sensorEventListener) | the listener to register |
| [callback] | [<code>errorFirstCallback</code>](#errorFirstCallback) | a node-style callback to notify the success or failure of the operation. |

**Example**  
```js
function listener(event) {
  console.log("device's rotation is " + event.values.join(','));
}

addSensorListener("ROTATION_VECTOR", "GAME", listener, function(error) {
  if (error) console.error("Could not listen to sensor");
})
```
<a name="sensors.removeSensorListener"></a>

### sensors.removeSensorListener(sensorType, samplingRate, listener, [callback]) ⇒ <code>undefined</code>
Remove a sensor listener.

**Kind**: static method of [<code>sensors</code>](#sensors)  

| Param | Type | Description |
| --- | --- | --- |
| sensorType | <code>string</code> | the type of the sensor (see [addSensorListener](#sensors.addSensorListener)) |
| samplingRate | <code>string</code> | the sampling period (see [addSensorListener](#sensors.addSensorListener)) |
| listener | [<code>sensorEventListener</code>](#sensorEventListener) | the listener to remove |
| [callback] | [<code>errorFirstCallback</code>](#errorFirstCallback) | a node-style callback to notify the success or failure of the operation. |

**Example**  
```js
removeSensorListener("ROTATION_VECTOR", "GAME", listener, function(error) {
  if (error) console.error("Could not stop listening to sensor");
})
```
<a name="SensorEvent"></a>

## SensorEvent : <code>Object</code>
Event emitted from sensors.

**Kind**: global typedef  
**Properties**

| Name | Type | Description |
| --- | --- | --- |
| sensor | <code>string</code> | The type of sensor that is listened to. |
| sampling | <code>string</code> | The sampling period the sensor is listened to by the receiving event listener. |
| timeStamp | <code>int</code> | The time the event was emitted. |
| values | <code>Array.&lt;float&gt;</code> | The sensor values. |

<a name="errorFirstCallback"></a>

## errorFirstCallback : <code>function</code>
This callback is used to get responses from async calls. It complies with
nodeJS callback style.

**Kind**: global typedef  

| Param | Type | Description |
| --- | --- | --- |
| [err] | <code>\*</code> | the error or undefined if everything went fine |
| data | <code>\*</code> | the response or the called function |

<a name="sensorEventListener"></a>

## sensorEventListener : <code>function</code>
This listener is used to receive events from sensors.

**Kind**: global typedef  

| Param | Type | Description |
| --- | --- | --- |
| evt | [<code>SensorEvent</code>](#SensorEvent) | the event emitted by one of the sensor |

