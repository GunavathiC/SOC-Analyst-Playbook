🔐 Detecting SSH Brute-Force Attacks Using Elastic Stack (ELK SIEM)
Introduction

SSH (Secure Shell) logs provide critical information about remote login attempts to servers. Monitoring SSH activity is essential for detecting brute-force attacks and unauthorized access attempts.

In this project, we use the Elastic Stack (Elasticsearch + Kibana + Logstash) to:

Ingest SSH logs

Detect multiple failed login attempts

Trigger alert rules

Send email notifications

Visualize alerts in a SOC dashboard

Project Overview

This project demonstrates a mini SOC monitoring pipeline built using Elastic Stack.

The system:

Collects SSH logs

Detects brute-force behavior

Generates alerts

Sends email notifications

Visualizes alert activity in Kibana

Prerequisites

Before starting, ensure:

Elasticsearch installed and running

Kibana installed and accessible (http://localhost:5601
)

Logstash configured for SSH log ingestion

Sample SSH logs available

Gmail SMTP configured for email alerts

Steps to Ingest SSH Logs into Elastic
1. Prepare Sample SSH Logs

Obtain sample SSH log file.

Ensure logs contain:

Timestamp

Source IP

Username

Login status (success / failed)

Place log file in Logstash accessible directory.

2. Configure Logstash Pipeline

Edit:

/etc/logstash/conf.d/ssh.conf

Example pipeline:

input {
  file {
    path => "/var/log/ssh.log"
    start_position => "beginning"
  }
}

filter {
  grok {
    match => { "message" => "%{SYSLOGTIMESTAMP:timestamp} %{HOSTNAME:host} sshd.* %{GREEDYDATA:action}" }
  }
}

output {
  elasticsearch {
    hosts => ["localhost:9200"]
    index => "ssh-logs"
  }
}

Restart Logstash:

sudo systemctl restart logstash
3. Verify Log Ingestion

Open Kibana → Dev Tools:

GET ssh-logs/_search

Confirm documents are indexed.

Steps to Create Brute-Force Detection Rule
1. Create Elasticsearch Query Rule

Go to:

Stack Management → Rules → Create Rule

Select:

Elasticsearch Query Rule

2. Configure Rule

Index: ssh-logs

Query:

message: "Failed password"

Condition:

Trigger alert when:

Count >= 5
within 1 minute
3. Configure Action Frequency

Set:

On status changes

This prevents continuous email spam.

Steps to Configure Email Notification
1. Create Email Connector

Go to:

Stack Management → Connectors → Create Connector

Select:

Email

2. Gmail SMTP Settings

Service: Gmail

Host: smtp.gmail.com

Port: 465

Secure: Enabled

Authentication: Enabled

Username: your_email@gmail.com

Password: App Password

3. Test Connector

Click Run Test
Ensure test email is received.

Steps to Create SOC Dashboard
1. Create Alerts Data View

Go to:

Stack Management → Data Views → Create Data View

Index Pattern:

.alerts-*

Enable:

 Allow hidden and system indices

Save data view.

2. Create Alert Trend Visualization

In Lens:

Data view → Alerts

X-axis → @timestamp

Y-axis → Count of records

Time → Last 24 hours

Save as:

Alert Trend (24h)
3. Create Total Alerts Metric

Visualization → Metric

Primary Metric → Count of records

Remove breakdown fields

Save as:

Total Alerts (24h)
4. Create Alerts by Rule Panel

Horizontal axis → kibana.alert.rule.name

Vertical axis → Count of records

Chart type → Bar

Save as:

Alerts by Rule
Detection Logic

The rule detects:

Multiple failed SSH login attempts

From same source IP

Within short time window

This indicates potential brute-force attack.

Key Learnings

Difference between .alerts-* and .kibana-alerts-*

Action frequency configuration

Alert lifecycle (Active → Recovered)

Email connector troubleshooting

Hidden system indices handling

SOC dashboard design principles

Conclusion

This project demonstrates how Elastic Stack can be used as a SIEM platform to:

Monitor SSH access

Detect brute-force attacks

Send automated email alerts

Visualize security incidents

It replicates a real-world SOC alerting workflow.
