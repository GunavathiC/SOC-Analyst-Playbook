🔐 SOC Alerting Dashboard using Elastic Stack
📌 Project Overview

This project demonstrates a Security Operations Center (SOC) monitoring pipeline built using the Elastic Stack (ELK).

It detects SSH brute-force login attempts, generates alerts, sends email notifications, and visualizes alert activity in a SOC dashboard.

🏗 Architecture

Log Source → Elasticsearch → Alert Rule → Email Connector → Dashboard Visualization

🛠 Tools Used

Elasticsearch

Kibana

Logstash

Gmail SMTP (Email Connector)

Kali Linux (log generation)

🚨 Detection Logic

Monitors SSH logs

Detects multiple failed login attempts

🎯 Skills Demonstrated

Threat detection engineering

Alert configuration

Email notification setup

Dashboard creation

Elastic Dev Tools usage

Troubleshooting alert pipelines

Triggers alert when threshold exceeded

Sends email notification
