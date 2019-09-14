

### Download Source and Javadoc

```groovy
eclipse {
    classpath {
        downloadJavadoc = true
        downloadSources = true
    }
}

idea {
    module {
        downloadJavadoc = true
        downloadSources = true
    }
}
```

### Integration Testing

```
testLogging.showStandardStreams = true
```

### Java Compatibility

```
sourceCompatibility = 1.8
targetCompatibility = 1.8
```

### Repositories

```
repositories {
    // Use -PuseMavenLocal=true to enable
    if (project.hasProperty("useMavenLocal")) {
        mavenLocal()
    }

    mavenCentral()
    jcenter()
    maven {
        credentials {
            username ''
            password ''
        }
        url ''
    }
}
```