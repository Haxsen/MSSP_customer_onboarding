# MSSP_customer_onboarding
## SentinelFlow: Automated MSSP Stack
### Stack: Wazuh (SIEM), Directus (Control Plane), n8n (Automation), Docker.

### The Problem: Manual onboarding for security clients is slow.
### The Solution: I built a pipeline where adding a client to the Directus DB automatically provisions security groups and API keys in Wazuh via n8n.

## Key Skills Demonstrated:

- Multi-component Docker Orchestration.

- API-first integration (Wazuh API).

- Security automation & SOC workflows.

## How to run the stack
### Run the docker stack
(create directories and allow access for the volumes being mounted [see docker compose] before running compose)
```bash
cd sentinelflow
docker compose up -d
```

### Run the security initialization
```bash
docker exec -it sentinelflow-wazuh-indexer-1 env JAVA_HOME=/usr/share/wazuh-indexer/jdk /bin/bash /usr/share/wazuh-indexer/plugins/opensearch-security/tools/securityadmin.sh \
  -cd /usr/share/wazuh-indexer/opensearch-security/ \
  -icl -nhnv \
  -cacert /usr/share/wazuh-indexer/certs/root-ca.pem \
  -cert /usr/share/wazuh-indexer/certs/admin.pem \
  -key /usr/share/wazuh-indexer/certs/admin-key.pem \
  -h localhost
```

### Run the cloudflare tunnel
See [cloudflare readme](./cloudflare/readme.md).

### Verify the stack
#### Wazuh
`xx.trycloudflare.com`
#### n8n
`http://localhost:5678/`
#### Directus
`http://localhost:8055/`

See docker compose for the creds / configure them yourself as needed.

# Sample built by haxsen
