# Smart Wildlife Habitat Monitoring System

A real-time IoT monitoring system built with Node-RED and MQTT to monitor environmental conditions across multiple wildlife habitats. The system processes simulated temperature, water-level, and motion data, evaluates habitat conditions, and displays live readings and threshold-based alerts through an interactive dashboard.

## Features

- Real-time monitoring of three wildlife habitat zones.
- Simulated temperature, water-level, and motion sensor data.
- MQTT publish-subscribe communication using separate topics for each sensor.
- Threshold-based classification into Stable, Warning, and Critical states.
- Color-coded status cards for rapid condition assessment.
- Dedicated dashboard pages with live readings for each habitat.
- MQTT alert messages containing the zone, status, alert details, and timestamp.
- Preconfigured demo controls for testing Stable, Warning, and Critical scenarios.
- Public EMQX MQTT broker integration.
- Five-second automatic sensor-update intervals.

## Monitored Wildlife Zones

| Zone | Habitat | Monitored Species |
|---|---|---|
| Zone 1 | Leopard Highlands | Arabian Leopard |
| Zone 2 | Oryx Plains | Arabian Oryx |
| Zone 3 | Gazelle Valley | Arabian Gazelle |

## System Workflow

1. Node-RED Inject nodes start the sensor simulation.
2. Function nodes generate temperature, water-level, and motion values.
3. MQTT Out nodes publish each sensor value to its dedicated topic.
4. MQTT In nodes receive the published data.
5. Function nodes evaluate the sensor values against configured thresholds.
6. The system assigns each zone a Stable, Warning, or Critical status.
7. Live readings, statuses, and alert messages are displayed on the dashboard.

## Alert Thresholds

| Sensor | Warning Condition | Critical Condition |
|---|---|---|
| Temperature | Above 42°C | Above 45°C |
| Water Level | Low | Empty |
| Motion | — | Intruder detected |

Critical conditions take priority over warning conditions when calculating the overall status of a zone.

## MQTT Topic Structure

Each zone uses separate MQTT topics for temperature, water level, motion, and alerts.

```text
wildlife/zone1/temperature
wildlife/zone1/water
wildlife/zone1/motion
wildlife/zone1/alerts

wildlife/zone2/temperature
wildlife/zone2/water
wildlife/zone2/motion
wildlife/zone2/alerts

wildlife/zone3/temperature
wildlife/zone3/water
wildlife/zone3/motion
wildlife/zone3/alerts
```

The system connects to the public EMQX broker:

```text
broker.emqx.io:1883
```

## Dashboard

The FlowFuse Dashboard provides:

- A reserve overview page showing the status of all wildlife zones.
- Dedicated detail pages for each habitat.
- Live temperature gauges.
- Water-level and motion readings.
- Color-coded status and alert messages.
- Stable, Warning, and Critical scenario controls for testing.

The dashboard is available at:

```text
http://localhost:1880/dashboard
```

## Repository Contents

- `wildlife_habitat_monitoring_flow.json` — complete Node-RED flow containing the sensor simulation, MQTT communication, threshold evaluation, alert handling, and dashboard configuration.

## Requirements

- Node.js
- Node-RED
- FlowFuse Dashboard 2.0 (`@flowfuse/node-red-dashboard`)
- Internet connection for the public MQTT broker

## Installation

Install Node-RED:

```bash
npm install -g node-red
```

Start Node-RED:

```bash
node-red
```

Open the Node-RED editor:

```text
http://localhost:1880
```

From the Node-RED menu:

1. Select **Manage Palette**.
2. Open the **Install** tab.
3. Search for `@flowfuse/node-red-dashboard`.
4. Install the FlowFuse Dashboard package.

## Import and Run

Clone the repository:

```bash
git clone https://github.com/r26th/smart-wildlife-habitat-monitoring.git
cd smart-wildlife-habitat-monitoring
```

Then:

1. Open the Node-RED editor.
2. Select **Menu → Import**.
3. Import `wildlife_habitat_monitoring_flow.json`.
4. Review the imported flow and click **Deploy**.
5. Open `http://localhost:1880/dashboard`.

The system will begin generating sensor readings and updating the dashboard automatically.

## Sensor Simulation

The project generates sensor data within Node-RED, allowing the complete MQTT workflow, threshold logic, dashboards, and alert scenarios to be tested consistently without requiring external hardware.
