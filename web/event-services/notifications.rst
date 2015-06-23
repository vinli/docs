Notifications
~~~~~~~~~~~~~

Notification state is useful in debugging notification handlers on your App.  This state property (as well as the `response` property) will inform you as to the result of Event Services' attempt to call the notification URL.


{
    "notifications": [
        {
            "id": "c12418d5-d1c9-4470-96eb-a6cf52185230",
            "eventId": "afe5b914-58ab-4701-8e24-56dccbda301a",
            "eventType": "rule-leave",
            "eventTimestamp": "2015-06-16T13:12:34.000Z",
            "subscriptionId": "cedeb7c2-cfd2-4087-8976-3bb3bad8cbb3",
            "responseCode": 201,
            "response": "{\"message\":{\"id\":\"SMd19c47b4ca2c4dd7964ad4b70cb97f9a\",\"to\":\"+15042207366\",\"from\":\"+12143909033\",\"body\":\"From Beagle: Test Device has left \\\"Marlee\\\"\",\"status\":\"queued\",\"errorCode\":null,\"errorMessage\":null}}",
            "url": "https://beagle-dev.vin.li/api/v1/notifications",
            "payload": "{\"notification\":{\"event\":{\"id\":\"afe5b914-58ab-4701-8e24-56dccbda301a\",\"timestamp\":\"2015-06-16T13:12:34.000Z\",\"deviceId\":\"fe4bbc20-cc90-11e3-8e05-f3abac5b60ff\",\"stored\":\"2015-06-16T13:12:35.825Z\",\"storageLatency\":1825,\"eventType\":\"rule-leave\",\"meta\":{\"direction\":\"leave\",\"firstEval\":false,\"rule\":{\"id\":\"41d68c9e-2914-4923-8593-3abdf299537c\",\"name\":\"[geofence] Marlee\",\"deviceId\":\"fe4bbc20-cc90-11e3-8e05-f3abac5b60ff\",\"boundaries\":[],\"evaluated\":true,\"covered\":false,\"createdAt\":\"2015-06-16T12:54:09.601Z\",\"links\":{\"self\":\"https://rules-dev.vin.li/api/v1/rules/41d68c9e-2914-4923-8593-3abdf299537c\",\"events\":\"https://events-dev.vin.li/api/v1/devices/fe4bbc20-cc90-11e3-8e05-f3abac5b60ff/events?type=rule&objectId=41d68c9e-2914-4923-8593-3abdf299537c\",\"subscriptions\":\"https://events-dev.vin.li/api/v1/devices/fe4bbc20-cc90-11e3-8e05-f3abac5b60ff/subscriptions?objectType=rule&objectId=41d68c9e-2914-4923-8593-3abdf299537c\"}},\"message\":{\"id\":\"cd339f3d-b0d8-49a9-a87d-ca7ee3a937e2\",\"timestamp\":\"2015-06-16T13:12:34.000Z\",\"snapshot\":{\"location\":{\"lat\":32.9745468870112,\"lon\":-96.9689222519258},\"vehicleSpeed\":0}}},\"object\":{\"id\":\"41d68c9e-2914-4923-8593-3abdf299537c\",\"type\":\"rule\",\"appId\":\"b75afd8f-7247-46e6-a0f9-04f187c9d9bd\"}},\"subscription\":{\"id\":\"cedeb7c2-cfd2-4087-8976-3bb3bad8cbb3\",\"deviceId\":\"fe4bbc20-cc90-11e3-8e05-f3abac5b60ff\",\"eventType\":\"rule-leave\",\"url\":\"https://beagle-dev.vin.li/api/v1/notifications\",\"object\":{\"id\":\"41d68c9e-2914-4923-8593-3abdf299537c\",\"type\":\"rule\"},\"appData\":\"{\\\"phoneNumber\\\":\\\"+15042207366\\\",\\\"body\\\":\\\"From Beagle: Test Device has left \\\\\\\"Marlee\\\\\\\"\\\",\\\"skipFirstEval\\\":true}\"}}}",
            "state": "complete",
            "notifiedAt": "2015-06-16T13:12:35.862Z",
            "respondedAt": "2015-06-16T13:12:36.300Z",
            "createdAt": "2015-06-16T13:12:35.842Z",
            "links": {
                "self": "https://events-dev.vin.li/api/v1/notifications/c12418d5-d1c9-4470-96eb-a6cf52185230",
                "event": "https://events-dev.vin.li/api/v1/devices/fe4bbc20-cc90-11e3-8e05-f3abac5b60ff/events/afe5b914-58ab-4701-8e24-56dccbda301a",
                "subscription": "https://events-dev.vin.li/api/v1/devices/fe4bbc20-cc90-11e3-8e05-f3abac5b60ff/subscriptions/cedeb7c2-cfd2-4087-8976-3bb3bad8cbb3"
            }
        }
    ],
    "meta": {
        "pagination": {
            "total": 1,
            "limit": 20,
            "offset": 0,
            "links": {
                "first": "https://events-dev.vin.li/api/v1/devices/fe4bbc20-cc90-11e3-8e05-f3abac5b60ff/subscriptions/cedeb7c2-cfd2-4087-8976-3bb3bad8cbb3/notifications?offset=0&limit=20",
                "last": "https://events-dev.vin.li/api/v1/devices/fe4bbc20-cc90-11e3-8e05-f3abac5b60ff/subscriptions/cedeb7c2-cfd2-4087-8976-3bb3bad8cbb3/notifications?offset=0&limit=20"
            }
        }
    }
}