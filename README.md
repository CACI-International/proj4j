# Proj4J

Proj4J is a Java library for converting coordinates between different geospatial coordinate reference systems.
It is designed to be compatible with `proj.4` parameters and derives some of its implementation from the `proj.4` sources.

Proj4J is a project in the [LocationTech](http://www.locationtech.org) working group of the Eclipse Foundation.

![LocationTech](locationtech_mark.png) 

## User Guide

Proj4J artifacts are available on maven central.

### Using Proj4J with Maven

To include Proj4J in a Maven project, add a dependency block like the following:

```xml
<properties>
    <proj4j.version>1.1.3</proj4j.version>
</properties>
<dependency>
    <groupId>org.locationtech.proj4j</groupId>
    <artifactId>proj4j</artifactId>
    <version>${proj4j.version}</version>
</dependency>
```

### Using Proj4J with Gradle

To include Proj4J in a Gradle project, add a dependency block like the following:

```
dependencies {
    implementation 'org.locationtech.proj4j:proj4j:1.1.3'
}
```

### Basic Usage

The following examples give a quick intro on how to use Proj4J in common
use cases.

#### Transforming coordinates from WGS84 to UTM

##### Obtaining CRSs by name

```Java
CRSFactory crsFactory = new CRSFactory();
CoordinateReferenceSystem WGS84 = crsFactory.createFromName("epsg:4326");
CoordinateReferenceSystem UTM = crsFactory.createFromName("epsg:25833");
```

##### Obtaining CRSs using parameters

```Java
CRSFactory crsFactory = new CRSFactory();
CoordinateReferenceSystem WGS84 = crsFactory.createFromParameters("WGS84",
    "+proj=longlat +datum=WGS84 +no_defs");
CoordinateReferenceSystem UTM = crsFactory.createFromParameters("UTM",
    "+proj=utm +zone=33 +ellps=GRS80 +towgs84=0,0,0,0,0,0,0 +units=m +no_defs");
```

##### Transforming coordinates

```Java
CoordinateTransformFactory ctFactory = new CoordinateTransformFactory();
CoordinateTransform wgsToUtm = ctFactory.createTransform(WGS84, UTM);
// `result` is an output parameter to `transform()`
ProjCoordinate result = new ProjCoordinate();
wgsToUtm.transform(new ProjCoordinate(lon, lat), result);
```

## Building, Testing and installing locally

`mvn clean install`

## Contributing

If you are interested in contributing to Proj4J please read the [**Contributing Guide**](CONTRIBUTING.md).
