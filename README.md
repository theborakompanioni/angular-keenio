[![Build Status](https://travis-ci.org/theborakompanioni/angular-keenio.svg?branch=master)](https://travis-ci.org/theborakompanioni/angular-keenio)

angular-keenio
=================

[Keen.io](https://keen.io/docs/data-visualization/) directives for Angular.js.

### Demo
See some examples on the [demo page](https://theborakompanioni.github.io/angular-keenio/).


### Installation
#### Configuration

```javascript
.config(['tbkKeenConfigProvider', function(tbkKeenConfigProvider) {
  var config = {
    projectId: "<MY_PROJECT_ID>",
    readKey: "<MY_READ_KEY>",
    writeKey: "<MY_WRITE_KEY>"
  };

  tbkKeenConfigProvider
    .projectId(config.projectId)
    .readKey(config.readKey)
    .writeKey(config.writeKey);
}])
```

#### Manually bootstrap application
`Keen` must be ready for the directives to work properly.
Bootstrap your angular application manually e.g.
```
<script>
  angular.element(document).ready(function () {
    Keen.ready(function () {
      angular.bootstrap(document, ['myApp']);
    });
  });
</script>
```

### Create Events

```javascript
.controller('MyController', [
'$scope', 'tbkKeen', function($scope, Keen) {
  Keen.addEvent('collectionName', {
    here:  'are',
    your: 'properties'
  })
  .then(function(res) {
    console.log(res);
  })
  .catch(function (err) {
    console.error(err);
  });
}]);
```

### Display charts

##### html
```html
<div data-tbk-keen-piechart 
  query="query" 
  height="250" 
  width="auto" 
  chart-options="chartOptions" 
></div>
```

##### controller
```javascript
.controller('myPageviewsByBrowserPiechartCtrl', [
'$scope', 'tbkKeen', function($scope, Keen) {
  $scope.query = new Keen.Query("count", {
    eventCollection: "pageviews",
    groupBy: "user.device_info.browser.family",
    timeframe: {
      start: "2014-05-01T00:00:00.000Z",
      end: "2014-05-05T00:00:00.000Z"
    }
  });

  $scope.chartOptions = {
    chartArea: {
      height: "85%",
      left: "5%",
      top: "5%",
      width: "100%"
    },
    pieHole: 0.4
  };
}]);
```




Contribute
------------

- Issue Tracker: https://github.com/theborakompanioni/angular-keenio/issues
- Source Code: https://github.com/theborakompanioni/angular-keenio

### Clone Repository
`git clone https://github.com/theborakompanioni/angular-keenio.git`


License
-------

The project is licensed under the MIT license. See
[LICENSE](https://github.com/theborakompanioni/angular-keenio/blob/master/LICENSE) for details.
