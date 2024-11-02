# [Resource Monitoring ](https://www.cloudskillsboost.google/games/5632/labs/36136)

# # Like, comment, share & Don't forget to subscribe [Qwiklab_Explorers_ts](https://youtube.com/@titashshil?si=RgamNu1dc9jVIbJN) 👍😄🤝

### Run the following Commands in CloudShell

```
cat > email-channel.json <<EOF_END
{
  "type": "email",
  "displayName": "qwiklab_explorers",
  "description": "Excillent",
  "labels": {
    "email_address": "$USER_EMAIL"
  }
}
EOF_END

gcloud beta monitoring channels create --channel-content-from-file="email-channel.json"

# Get the channel ID
email_channel_info=$(gcloud beta monitoring channels list)
email_channel_id=$(echo "$email_channel_info" | grep -oP 'name: \K[^ ]+' | head -n 1)

cat > qwiklab_explorers_lab.json <<EOF_END
{
  "displayName": "qwiklab_explorers",
  "userLabels": {},
  "conditions": [
    {
      "displayName": "VM Instance - CPU utilization",
      "conditionThreshold": {
        "filter": "resource.type = \"gce_instance\" AND metric.type = \"compute.googleapis.com/instance/cpu/utilization\"",
        "aggregations": [
          {
            "alignmentPeriod": "60s",
            "crossSeriesReducer": "REDUCE_NONE",
            "perSeriesAligner": "ALIGN_MEAN"
          }
        ],
        "comparison": "COMPARISON_GT",
        "duration": "0s",
        "trigger": {
          "count": 1
        },
        "thresholdValue": 0.2
      }
    },
    {
      "displayName": "VM Instance - CPU utilization",
      "conditionThreshold": {
        "filter": "resource.type = \"gce_instance\" AND metric.type = \"compute.googleapis.com/instance/cpu/utilization\"",
        "aggregations": [
          {
            "alignmentPeriod": "60s",
            "crossSeriesReducer": "REDUCE_NONE",
            "perSeriesAligner": "ALIGN_MEAN"
          }
        ],
        "comparison": "COMPARISON_GT",
        "duration": "0s",
        "trigger": {
          "count": 1
        },
        "thresholdValue": 0.2
      }
    }
  ],
  "alertStrategy": {
    "notificationPrompts": [
      "OPENED"
    ]
  },
  "combiner": "AND_WITH_MATCHING_RESOURCE",
  "enabled": true,
  "notificationChannels": [
    "$email_channel_id"
  ],
  "severity": "SEVERITY_UNSPECIFIED"
}
EOF_END

# Create the alert policy
gcloud alpha monitoring policies create --policy-from-file=qwiklab_explorers_lab.json
```
---

* Go to **Dashboards Overview** from [here](https://console.cloud.google.com/monitoring/dashboards?)

* In Metric field dropdown :
```
CPU utilization
```

* Go to **Create group** from [here](https://console.cloud.google.com/monitoring/groups/create?)

* Enter a name for the group :
```
VM instances
```

* In the Criteria section :
```
nginx
```

* Go to **Create Uptime Check** from [here](https://console.cloud.google.com/monitoring/uptime/create?)

---

# Congratulations ..!!🎉  You completed the lab shortly..😃💯

# *Well done..!* 👏

# Thank you for visiting.... :) 🗯️

# [Qwiklab_Explorers_ts](https://youtube.com/@titashshil?si=RgamNu1dc9jVIbJN)
