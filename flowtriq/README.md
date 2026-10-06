# Flowtriq Agent

## From the [Flowtriq](https://flowtriq.com) website

DDoS detection agent running in flow collector mode. Receives sFlow, NetFlow v5/v9, or IPFIX exports from your router or switch and reports to your Flowtriq dashboard for alerting and incident management.

This egg runs the agent as a flow collector, not as a local traffic monitor. It listens on the server's primary port for incoming flow data from your network equipment. The agent parses the flows, builds traffic baselines, detects volumetric attacks, and reports to your dashboard.

## Requirements

You need a Flowtriq account to use this egg. Sign up at [flowtriq.com](https://flowtriq.com) and create a node in your dashboard to get an API key and Node UUID.

Your router or switch must support sFlow, NetFlow v5/v9, or IPFIX export. Configure it to send flows to this server's IP on the allocated port.

## Minimum Resources

| Resource | Minimum   |
|----------|-----------|
| CPU      | 1 core    |
| RAM      | 256 MB    |
| Disk     | 500 MB    |

## Server Ports

The flow collector listens on the server's primary allocated port (UDP). Set your allocation port to 2055 for NetFlow, 6343 for sFlow, or 4739 for IPFIX.

| Port              | default | protocol |
|-------------------|---------|----------|
| Flow collector    | 2055    | UDP      |

## Variables

| Variable          | Description                                                         | Default  | Required |
|-------------------|---------------------------------------------------------------------|----------|----------|
| API Key           | Your Flowtriq API key from the dashboard                            |          | Yes      |
| Node UUID         | The UUID for this node, created in your Flowtriq dashboard          |          | Yes      |
| Flow Protocol     | auto, sflow, netflow_v5, netflow_v9, or ipfix                      | auto     | Yes      |
| API Base URL      | API endpoint (only change for self-hosted instances)                | https://flowtriq.com/api/v1 | Yes |

## How It Works

1. Pelican allocates a port for this server (e.g. 2055)
2. The agent starts and listens on that port for incoming flow data
3. Configure your router/switch to export flows to this server's IP and port
4. The agent parses flows, learns traffic baselines, and detects attacks
5. Incidents and traffic stats appear in your Flowtriq dashboard
