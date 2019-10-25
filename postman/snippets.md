---
layout: guide
title: "Postman Fundamentals"
subject: postman
---

# Postman Fundamentals

List of URLs and code snippets to follow along with the Postman Fundamentals lab.

## Milestone 0
[Download the API Client](https://www.getpostman.com/apps)

## Milestone 1
cURL: Google
```
curl --X GET 'https://www.google.com/' >> get_google.html
open get_google.html
```

Postman: Google
```
GET https://www.google.com/
```

Documentation: OpenWeatherMap Current Weather Data API
```
https://openweathermap.org/current
```

Postman: OpenWeatherMap
```
GET https://api.openweathermap.org/data/2.5/weather?APPID=bdccc7424e97e0977392a147f3dee1a7&q=Pittsburgh
```

cURL: OpenWeatherMap
```
curl -X GET 'https://api.openweathermap.org/data/2.5/weather?APPID=bdccc7424e97e0977392a147f3dee1a7&q=Pittsburgh'
```

## Milestone 2
Documentation: Restful-booker
```
https://restful-booker.herokuapp.com/apidoc/index.html
```

Postman: Get All Bookings
```
GET https://restful-booker.herokuapp.com/booking
```

Postman: Create a Booking
```
POST https://restful-booker.herokuapp.com/booking
```

Booking Information (Body → Raw → JSON)
```
{
    "firstname": "John",
    "lastname": "Appleseed",
    "totalprice": 15151,
    "depositpaid": true,
    "bookingdates": {
        "checkin": "2019-10-25",
        "checkout": "2019-10-26"
    }
}
```

Postman: Delete a Booking
```
DELETE https://restful-booker.herokuapp.com/booking/0
```

Postman: Authorization
```
POST https://restful-booker.herokuapp.com/auth
```

Credentials (Body → Raw → JSON)
```
{
    "username" : "admin",
    "password" : "password123"
}
```

Postman: Delete a Booking (successfully!)
```
DELETE https://restful-booker.herokuapp.com/booking/0
```

Authorization (Header)
```
{
    "cookie" : "token={{token}}"
}
```

## Milestone 3
Postman: Get all Bookings Test
```
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

pm.test("Response time is less than 200ms", function () {
    pm.expect(pm.response.responseTime).to.be.below(200);
});
```