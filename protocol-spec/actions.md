# Smart Electricity Meter Actions

This document describes the available actions that can be performed on a Smart Electricity Meter.

---

## CONNECT

**Operation:** Connect Electricity Supply

### Description

Reconnects the consumer's electricity supply through the meter. This action is typically used when the supply was previously disconnected due to exhausted prepaid balance, temporary suspension, or administrative disconnection.

### Effect

- Restores power supply to the consumer premises.
- Closes the internal disconnect relay of the meter.
- Does not affect network connectivity or communication status.

### Example Use Cases

- Consumer has successfully recharged their prepaid balance.
- Supply restoration after temporary suspension.
- Remote reconnection by utility operator.

---

## DISCONNECT

**Operation:** Disconnect Electricity Supply

### Description

Disconnects the consumer's electricity supply remotely through the meter. This operation may be used for unpaid dues, exhausted prepaid balance, maintenance activities, or administrative actions.

### Effect

- Stops electricity delivery to the consumer premises.
- Opens the internal disconnect relay of the meter.
- Meter communication remains active if communication infrastructure is available.

### Example Use Cases

- Prepaid balance exhausted.
- Outstanding payment issues.
- Emergency or maintenance shutdown.

---

## READ

**Operation:** Read Meter Data

### Description

Retrieves meter information and operational data from the device.

### Typical Data Includes

- Meter serial number
- Current meter status
- Energy consumption (kWh/kvah)
- Voltage readings
- Current readings
- Power factor
- Relay status

### Effect

- No configuration changes are performed.
- Read-only operation.

---

## SET_LOAD

**Operation:** Set Load Limit

### Description

Configures the maximum allowed load or demand threshold for the meter/consumer connection.

### Effect

- Updates the permissible load limit.
- Allows utility operators to enforce contracted load capacity.
- Can trigger alarms or protective actions when exceeded.

### Example Use Cases

- Load contract modification.
- Consumer plan upgrade or downgrade.
- Demand management operations.

---

## SET_PP

**Operation:** Set Password Protection Mode

### Description

Enables, disables, or modifies password protection settings for meter access.

### Effect

- Controls access to protected operations.
- Prevents unauthorized configuration changes.
- Enhances device security.

### Example Use Cases

- Initial meter commissioning.
- Security policy updates.
- Password protection activation.

---

## SET_ID

**Operation:** Set Meter Unit ID

### Description

Changes the communication address (Slave ID / Unit ID) assigned to the meter.

### Effect

- Updates the meter identifier used during communication.
- Future requests must use the newly assigned ID.

### Example Use Cases

- Network reconfiguration.
- Address conflict resolution.
- Meter replacement activities.

---

## FACTORY_RESET

**Operation:** Factory Reset

### Description

Restores configurable meter settings to factory defaults.

### Effect

- Resets communication and configuration parameters.
- Removes user-defined settings where supported.
- Returns the meter to its default operational state.

### Warning

Perform this operation only when necessary, as reconfiguration may be required afterward.

### Example Use Cases

- Device troubleshooting.
- Recommissioning.
- Configuration recovery.

---

## SET_RELAY

**Operation:** Set Relay State

### Description

Controls the internal relay state of the smart meter.

### Supported States
<!-- - `ON` (Relay Closed)
- `OFF` (Relay Open) -->

### Effect

- Directly changes the physical relay status.
- Depending on meter implementation, this may impact electricity supply availability.

### Example Use Cases

- Manual relay control.
- Testing and diagnostics.
- Utility control operations.

---

## PASS_RESET

**Operation:** Reset Default Password

### Description

Resets the meter password to the manufacturer-defined default credentials.

### Effect

- Removes the currently configured password.
- Restores default authentication settings.

### Warning

After password reset, configure a new secure password immediately to prevent unauthorized access.

### Example Use Cases

- Forgotten credentials.
- Device recovery.
- Administrative maintenance.

---

## Notes

### CONNECT vs DISCONNECT

These operations control the **electricity supply relay** inside the meter and **do not represent network connectivity**.

| Action | Result |
|----------|----------|
| CONNECT | Electricity supply is restored to the consumer. |
| DISCONNECT | Electricity supply is disconnected from the consumer. |

### Example Scenario

1. Electricity is available in the area.
2. Consumer's prepaid balance reaches zero.
3. Utility sends a `DISCONNECT` command.
4. Meter opens its internal relay and stops supplying electricity.
5. Consumer recharges the balance.
6. Utility sends a `CONNECT` command.
7. Meter closes the relay and restores electricity supply.

---