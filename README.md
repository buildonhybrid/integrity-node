# Integrity Node Deployment Guide

### Requirements

Make sure you have the following installed and set up:

- Docker
- docker-compose
- A `.env` file in the project root directory with the required environment variables

---

### Step 1: Clone and Configure

Clone the repository and move into the project directory:

```bash
git clone https://github.com/buildonhybrid/integrity-nodes.git
cd integrity-node
```

Create a `.env` file with the following contents:

```env
RPC_URL=<your_arb-sepolia_rpc_url>
OPERATOR_PRIVATE_KEY=<your_operator_private_key>
PROTOCOL_CONTRACT_ADDRESS=<protocol_contract_address>
```

---

### Step 2: Docker Compose Setup

The `docker-compose.yml` includes two services:

#### integrity-node

- Runs the core job processor
- Uses the `buildonhybrid/integrity-node` image
- Loads environment variables from `.env`
- Has labels configured for automatic updates

#### autoupdate (Watchtower)

- Uses the `containrrr/watchtower:1.7.1` image
- Polls every 3 hours for updates (`WATCHTOWER_POLL_INTERVAL=10800`)
- Only updates containers with specific labels (in this case, the hybrid-node)

---

### Step 3: Start the Node

To start everything:

```bash
docker-compose up -d
```

To view logs:

```bash
docker-compose logs -f integrity-node
```

---

### Step 4: Delegate Licenses

Once the node is running, go to the Delegation Page to delegate your licenses

> Each node can delegate up to **50 licenses per operator wallet**.

---

### Stopping and Restarting the Node

To stop everything:

```bash
docker-compose down
```

To rebuild and restart (for updates or config changes):

```bash
docker-compose down && docker-compose up -d --pull always
```
