OVERVIEW

Let S be the container which sends pings.
Let R be the container which responds to pings.
Let D be the discovery mechanism (whether it be in the host namespace or a
separate container.
Let R's service name be SERVICE_R.

what we need:
  1 container to respond to pings
  1 container to send pings


Steps
- S sends a hostname resolve request for SERVICE_R to D
- D performs service discovery and gets R's IP.
- D responds to S with the flowID (virtual IP) and creates a mapping of
  [flowID, R_IP, S_PORT]
- S sends a ping packet to R and R responds.
- A new instance of R is created

Notes:
- If we run S and R each in a separate network namespace, we can have an
  instance of D (the orchestrator) in each namespace which can intercept and
  manipulate requests