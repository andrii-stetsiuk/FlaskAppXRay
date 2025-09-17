# FlaskAppXRay

  Endpoints:
  
    - GET http://localhost/api/requests
      Example response:
      {
        "container_hostname": "28f26bfaf5df",
        "container_ip": "172.19.0.5",
        "total_count_of_requests": "237"
      }

    - GET http://localhost/api/health
      Example response:
      {
        "service_status": "pass/warning",
        "service_version": "1.0.5"
      }

  How to run:
    docker-compose up --build --scale flask-app=2 --remove-orphans

  AWS X-Ray integration:
    - The app is instrumented with AWS X-Ray SDK.
    - X-Ray daemon runs as a sidecar service `xray-daemon`.
    - Default region is `eu-central-1` (change `AWS_REGION` in compose if needed).
    - X-Ray UDP port is exposed at 2000/udp.
    - Environment variables used by the app:
        AWS_XRAY_DAEMON_ADDRESS=xray-daemon:2000
        AWS_XRAY_TRACING_NAME=FlaskApp
        AWS_REGION=eu-central-1

  View traces:
    - Ensure your AWS credentials on the host allow X-Ray PutTraceSegments.
    - Open AWS X-Ray console and filter by service name `FlaskApp`.
