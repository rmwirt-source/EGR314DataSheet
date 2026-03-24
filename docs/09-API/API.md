---
title: API — Controller Subsystem (Rylee)
---

## Overview

This page defines the Application Programming Interface (API) for the Controller Input subsystem (Node ID `0x04`).

This node is responsible for:
- Handling local user input (buttons / controls)
- Sending control commands to motor nodes
- Forwarding all network traffic in the daisy-chain
- Responding to system-level telemetry requests

All messages follow the **team-defined 64-byte packet structure**, with this page focusing only on the **message payload (bytes 4–61)**.

---

## Node Information

| Property | Value |
|--------|------|
| Node Name | Controller Input |
| Node ID | `0x04` |
| Role | Input + Routing Node |

---

# Messages Sent

---

## Message Type `0x0043` — Button Press

**Description:**  
Sent when a local button interaction occurs. This is forwarded to motor nodes and upstream logging systems.

| Field | Value |
|------|------|
| Bytes | 3+ |
| Message Type | `0x0043` |

| Byte Offset | Variable Name | Type | Min | Max |
|------------|--------------|------|-----|-----|
| 6 | button_id | uint8_t | 0 | 255 |
| 7 | press_type | uint8_t | 0 | 2 |
| 8 | sequence | uint8_t | 0 | 255 |

**Notes:**
- `press_type`: 0 = short, 1 = long, 2 = double
- Sequence is used for debounce tracking or event ordering

---

## Message Type `0x0001` — Set Motor Speed

**Description:**  
Controller-generated command sent to motor nodes.

| Field | Value |
|------|------|
| Bytes | 5 |
| Message Type | `0x0001` |

| Byte Offset | Variable Name | Type | Min | Max |
|------------|--------------|------|-----|-----|
| 6 | motor_id | uint8_t | 0 | 255 |
| 7–8 | speed | uint16_t | 0 | 1000 |
| 9 | direction | uint8_t | 0 | 1 |
| 10 | flags | uint8_t | 0 | 255 |

**Notes:**
- Speed is encoded as unsigned magnitude
- Direction determines forward or reverse

---

# Messages Received

---

## Message Type `0x0004` — ACK

**Description:**  
Acknowledgement for previously sent commands.

| Field | Value |
|------|------|
| Bytes | 3+ |
| Message Type | `0x0004` |

| Byte Offset | Variable Name | Type | Min | Max |
|------------|--------------|------|-----|-----|
| 6 | ack_type | uint8_t | 0 | 255 |
| 7 | status | uint8_t | 0 | 1 |
| 8 | error_code | uint8_t | 0 | 255 |

**Handling Behavior:**
- If `status = 0` → command successful
- If `status = 1` → error occurred, log error_code
- Generate debug output over UART

---

## Message Type `0x0005` — Error / Event Log

**Description:**  
System-wide error reporting.

| Byte Offset | Variable Name | Type | Min | Max |
|------------|--------------|------|-----|-----|
| 6 | error_code | uint8_t | 0 | 255 |
| 7 | severity | uint8_t | 0 | 3 |

**Handling Behavior:**
- Log error message
- Trigger warning indicator if severity ≥ 2

---

# Broadcast / Reactive Messages

---

## Message Type `0x0002` — Request Telemetry

**Description:**  
Broadcast request for system data.

| Byte Offset | Variable Name | Type | Min | Max |
|------------|--------------|------|-----|-----|
| 6 | telemetry_mask | uint8_t | 0 | 255 |
| 7 | timeout | uint8_t | 0 | 255 |

**Handling Behavior:**
- Controller does not generate sensor telemetry
- May respond with status if required
- Always forwards message

---

# Message Handling Implementation

## Receiver Requirements

The controller implements a UART-based message handler that:

- Reads incoming bytes continuously
- Detects valid packet framing (`0x41 0x5A ... 0x59 0x42`)
- Verifies message length
- Ignores malformed packets
- Drops packets originating from itself
- Forwards packets not addressed to `0x04`
- Processes valid messages addressed to this node

## Processing Logic

1. Check destination:
   - If `dst == 0x04` → process
   - Else → forward

2. If message is valid:
   - Parse message type
   - Extract payload fields
   - Execute corresponding handler

3. Send ACK:
   - Always respond to valid commands with `0x0004`

---

## Sender Requirements

The controller periodically sends:

- Button press events (`0x0043`)
- Motor commands (`0x0001`)

### Constraints

- Must respect max packet size (64 bytes)
- Must avoid reserved prefix/suffix values inside payload
- Must use correct source (`0x04`) and destination IDs
- Must be non-blocking and rate-limited

---

## Error Handling

The system safely ignores:

- Malformed packets
- Invalid message types
- Messages exceeding buffer size
- Unexpected payload values

Errors may trigger:
- UART debug print
- LED indicator (optional)

---

## Software Packaging

- Full firmware project is included as a `.zip`
- Code is structured for:
  - Message parsing
  - Routing
  - Command handling

---

## Summary

This API ensures that the Controller subsystem:

- Properly integrates into the team daisy-chain network
- Reliably sends user input commands
- Correctly processes acknowledgements and system messages
- Maintains robust communication through validation and error handling

---

## Downloads

- [Firmware ZIP](LINK_TO_ZIP)
