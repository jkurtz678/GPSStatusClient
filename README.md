# GPS Status Client

Web page built with Vue that displays the status of OneStepGPS devices.

Press 'latest points' button to update table with most recent data from the OneStepGPS API. The data values displayed include online/offline status, name associated with device, latest point location (latitude, longitude), and time since device was last updated. When the auto update checkbox is checked, the application will continuously update the table every five seconds. The table can also be sorted by chosen columns.

## Server Setup

Client makes requests to Go server at http://localhost:8080/latest to retrieve latest gps point coordinates. Go to https://github.com/jkurtz678/LatestPointsGoServer to set up the server. 


## Vue Client Setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
