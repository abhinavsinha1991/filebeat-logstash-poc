## Deploy logstash and filebeat first:

`kubectl apply -f deploy/`

## Login to the filebeat pod

`kubectl exec -it <filebeat-pod-name> bash`

## Add the following lines to a file in PWD by name *.log, e.g abc.log:

```
"321 - App01 - WebServer is starting"
"321 - App01 - WebServer is up and running"
"321 - App01 - WebServer is scaling 2 pods"
"789 - App02 - Database is will be restarted in 5 minutes"
"789 - App02 - Database is up and running"
"789 - App02 - Database is refreshing tables"
```

## Check logstash logs:

`kubectl logs -f logstash`

### The message field will have truncated service status as below:

```
{
      "@version" => "1",
       "service" => {
        "status" => "Datab",
           "pid" => 789,
          "name" => "App02"
    },
          "tags" => [
        [0] "beats_input_codec_plain_applied"
    ],
    "@timestamp" => 2021-05-30T12:52:01.213Z,
          "host" => {
        "name" => "minikube"
    },
           "ecs" => {
        "version" => "1.5.0"
    },
       "message" => "789 App02 Datab",
         "input" => {
        "type" => "log"
    },
         "agent" => {
                "type" => "filebeat",
            "hostname" => "minikube",
             "version" => "7.8.0",
                  "id" => "afa2af10-d24b-4d5c-b768-730c7035d1d6",
                "name" => "minikube",
        "ephemeral_id" => "afdcfa7d-b229-4e3e-b13f-4441709c3bf1"
    },
           "log" => {
         "flags" => [
            [0] "truncated"
        ],
        "offset" => 228,
          "file" => {
            "path" => "/usr/share/filebeat/hhh.log"
        }
    }
}
```