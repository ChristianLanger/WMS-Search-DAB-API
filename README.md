## WMS Search GEO DAB API

A web tool to search for Web Mapping Services (WMS) inside the GEO Discovery Access Broker API (http://www.geodab.net)

## Getting Started

These instructions based on the Javascript API will get you a copy of the project up and running on your local machine for development and testing purposes.

```

// creates a new DAB instance with the given endpoint
    var dab = GIAPI.DAB('http://api.eurogeoss-broker.eu/dab');

    // defines discover response callback function
    var onResponse = function(response){
    	
    	// retrieves the result set
    	// only one result set is expected (discover not expanded)     
        var resultSet = response[0];
    	
    	if(resultSet.error){
    	     document.writeln("Error occurred: "+resultSet.error); 
             return;
        }
        
        // retrieves the paginator   
        var paginator = resultSet.paginator;
                        
        // prints the result set
        document.writeln("<h3>- Result set -</h3>");
        document.writeln("start:"+resultSet.start+"<br>"); 
        document.writeln("size:"+resultSet.size+"<br>"); 
        document.writeln("pageCount:"+resultSet.pageCount+"<br>"); 
        document.writeln("pageIndex:"+resultSet.pageIndex+"<br>"); 
        document.writeln("pageSize:"+resultSet.pageSize+"<br>"); 
 
        // the current paginator page (the first of the result set)    
        var page = paginator.page();
        
        // printing page nodes
        document.writeln("<h3>- Nodes of first result set page-</h3>"); 
        document.writeln("<pre>"); 

        while(page.hasNext()){

            // retrieving the next page node
            var node = page.next();
        
            // retrieving the node report
            var report = node.report();     
                           
            document.writeln(JSON.stringify(report,null,4));
        }
        document.writeln("</pre>");
        document.close();
    };

    // discover constraints
    var constraints = {
        
        "where": {
            "south": 40,
            "west": -3,
            "north": 46,
            "east": 26
         },
         
         "when": {
             "from": "2000-01-01",
             "to": "2013-01-01"
         },
         
         "what": "temperature"               
    };
    
    // set page size
    var options = {
        
        "pageSize": 5           
    };
                
    // start discover
    dab.discover(onResponse, constraints, options);

```

## What is the GEO DAB

Description from the official page http://www.geodab.net

```
GEO DAB is a key component of the GEOSS Common Infrastructure (GCI), transparently connecting GEOSS User’s 
requests to the resources shared by the GEOSS Providers.

GEO DAB scope is to simplify cross and multi-disciplinary discovery, access, and use (or reuse) 
of disparate data and information.

GEO DAB is a brokering framework that interconnects hundreds of heterogeneous and autonomous supply 
systems (the enterprise systems constituting the GEO metasystem) by providing mediation, 
harmonization, transformation, and QoS capabilities.
```

## Built With

* [GEO DAB API](http://api.eurogeoss-broker.eu/docs/index.html) - DAB Javascript API
* [Leaflet JS](http://leafletjs.com/) - Leaflet JS
* [Mapbox JS API](https://www.mapbox.com/mapbox-gl-js/api/#geolocatecontrol) - Mapbox Geolocate API
* [Bootstrap](http://getbootstrap.com/) - HTML, CSS, JS web framework

## Demo

See a [Demo](http://rawgit.com/ChristianLanger/WMS-Search-DAB-API/master/index.html) for details

