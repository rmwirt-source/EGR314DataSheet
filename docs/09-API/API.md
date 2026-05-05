---
title: API — Controller Subsystem (Rylee)
---

## API Design Explanation

The API was designed to provide a clear interface between the hardware and software components of the system. Each function corresponds to a specific subsystem operation, such as reading sensor data or transmitting information wirelessly.

The structure of the API ensures that all hardware interactions are abstracted into simple function calls. This improves code readability and makes the system easier to debug and maintain.

The API also aligns with the team communication protocol by ensuring that all transmitted data follows a consistent format. This allows different parts of the system to communicate reliably and ensures compatibility with other modules.

## Node Information

| Property | Value |
|---|---|
| Node Name | Controller Input |
| Node ID | `W` |
| ASCII Hex Value | `0x57` |
| Role | Input and Routing Node |

## Messages Sent

### Message Type `0x0043` — Button Press

**Description:**  
Sent when a local button interaction occurs.

| Byte Offset | Variable Name | Type | Min | Max | Example |
|---|---|---|---|---|---|
| 4 to 5 | message_type | uint16_t | `0x0043` | `0x0043` | `0x0043` |
| 6 | button_id | uint8_t | 0 | 255 | 1 |
| 7 | press_type | uint8_t | 0 | 2 | 0 |
| 8 | sequence | uint8_t | 0 | 255 | 12 |

**Notes:**  
* `press_type = 0` means short press  
* `press_type = 1` means long press  
* `press_type = 2` means double press

**Example payload:**  
`43 00 01 00 0C`

---

### Message Type `0x0001` — Set Motor Speed

**Description:**  
Command sent to motor nodes.

| Byte Offset | Variable Name | Type | Min | Max | Example |
|---|---|---|---|---|---|
| 4 to 5 | message_type | uint16_t | `0x0001` | `0x0001` | `0x0001` |
| 6 | motor_id | uint8_t | 0 | 255 | 1 |
| 7 to 8 | speed | uint16_t | 0 | 1000 | 250 |
| 9 | direction | uint8_t | 0 | 1 | 0 |
| 10 | flags | uint8_t | 0 | 255 | 0 |

**Notes:**  
* Speed is the magnitude of the command  
* Direction: `0 = forward`, `1 = reverse`

**Example payload:**  
`01 00 01 FA 00 00`

## Messages Received

### Message Type `0x0004` — ACK

**Description:**  
Acknowledgement for commands sent by this node.

| Byte Offset | Variable Name | Type | Min | Max | Example |
|---|---|---|---|---|---|
| 4 to 5 | message_type | uint16_t | `0x0004` | `0x0004` | `0x0004` |
| 6 | ack_type | uint8_t | 0 | 255 | 1 |
| 7 | status | uint8_t | 0 | 1 | 0 |
| 8 | error_code | uint8_t | 0 | 255 | 0 |

**Handling Behavior:**  
* `status = 0` means success  
* `status = 1` means error, log the error code

**Example payload:**  
`04 00 01 00 00`

---

### Message Type `0x0005` — Error / Event Log

**Description:**  
System wide error reporting.

| Byte Offset | Variable Name | Type | Min | Max | Example |
|---|---|---|---|---|---|
| 4 to 5 | message_type | uint16_t | `0x0005` | `0x0005` | `0x0005` |
| 6 | error_code | uint8_t | 0 | 255 | 2 |
| 7 | severity | uint8_t | 0 | 3 | 2 |

**Handling Behavior:**  
* Log the error
* Indicate a warning if severity is 2 or higher

**Example payload:**  
`05 00 02 02`

## Broadcast / Reactive Messages

### Message Type `0x0002` — Request Telemetry

**Description:**  
Broadcast request for system data.

| Byte Offset | Variable Name | Type | Min | Max | Example |
|---|---|---|---|---|---|
| 4 to 5 | message_type | uint16_t | `0x0002` | `0x0002` | `0x0002` |
| 6 | telemetry_mask | uint8_t | 0 | 255 | 31 |
| 7 | timeout | uint8_t | 0 | 255 | 5 |

**Handling Behavior:**  
* Forward the message
* This node does not generate direct telemetry

**Example payload:**  
`02 00 1F 05`

## Message Handling Implementation

### Receiver Behavior

The ESP32 firmware implements a UART message handler that:

* Continuously reads incoming bytes
* Detects valid packet framing
* Verifies packet length
* Ignores malformed packets
* Drops messages originating from itself
* Forwards messages not addressed to `W`
* Processes messages addressed to this node

### Processing Logic

1. Check destination.
   * If `dst == W`, process the message
   * Otherwise, forward it

2. Parse the message.
   * Identify the message type
   * Extract the payload data

3. Respond.
   * Send an ACK for valid messages received by this node

## Sender Behavior

The controller sends:

* Button press messages
* Motor speed commands
* Telemetry requests

### Constraints

* Maximum packet size is 64 bytes
* Payload must not exceed the specification
* Correct source and destination IDs are required
* Messages are rate limited and non blocking

## Error Handling

The system ignores:

* Malformed packets
* Invalid message types
* Oversized messages
* Unexpected payload values

Optional debug outputs:

* UART print statements
* LED indicators

## Software Packaging

* Full firmware project is included as a `.zip`
* Implemented for ESP32 platform
* Code structure includes:
  * UART communication
  * Packet parsing
  * Message routing
  * Command handling

## Summary

This API ensures that the Controller subsystem:

* Integrates with the team daisy chain network
* Sends valid control commands
* Correctly processes incoming messages
* Maintains reliable communication through validation and routing

## Downloads

* [ESP32 Firmware ZIP](LINK_TO_ZIP)
